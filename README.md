# lab3
wektory


#include <iostream>
using namespace std;

class Vector {
public:
	Vector(int size) : size(size) {
		arr = new double[size];
		for (int i = 0; i < size; i++) {
			arr[i] = 0;
		}
	}

	double& operator [](int w) {
		if (w<0 && w>size) throw std::invalid_argument("nie mam takiego elementu");
		return arr[w];
	}

	void operator =(Vector& other) {
		if (this == &other) {
			if (other.size != size) throw std::invalid_argument("to to samo");
		}
		memcpy(arr, other.arr, size * sizeof(double));
	}

	void operator =(Vector&& rhs) {
		size = rhs.size;
		arr = new double[size];
		memmove(arr, rhs.arr, size * sizeof(double));
	}

	Vector(Vector& other) : size(other.size) {
		arr = new double[size];
		memcpy(arr, other.arr, size * sizeof(double));
	}

	Vector& operator +(Vector& other) {
		if (other.size != size) throw std::invalid_argument("zly rozmiar");
		Vector result(size);
		for (int i = 0; i < size; i++) {
			result.arr[i] = arr[i] + other.arr[i];
			}
		return result;
	}
	Vector& operator -(Vector& other) {
		if (other.size != size) throw std::invalid_argument("zly rozmiar");
		Vector result(size);
		for (int i = 0; i < size; i++) {
			result.arr[i] = arr[i] - other.arr[i];
		}
		return result;
	}
	Vector& operator *(Vector& other) {
		if (other.size != size) throw std::invalid_argument("zly rozmiar");
		Vector result(size);
		for (int i = 0; i < size; i++) {
			result.arr[i] = arr[i] * other.arr[i];
		}
		return result;
	}

	Vector& operator /(double k) {
		Vector result(size);
		for (int i = 0; i < size; i++) {
			result.arr[i] = arr[i] / k;
		}
		return result;
	}

	Vector& operator *(double k) {
		Vector result(size);
		for (int i = 0; i < size; i++) {
			result.arr[i] = arr[i] * k;
		}
		return result;
	}

	Vector& operator /(Vector& other) {
		if (other.size != size) throw std::invalid_argument("zly rozmiar");
		Vector result(size);
		for (int i = 0; i < size; i++) {
			result.arr[i] = arr[i] / other.arr[i];
		}
		return result;
	}


	~Vector() {
		delete[] arr;
	}

private:
	double* arr;
	int size;
};

int main()
{
	Vector v(5);
	Vector v2 = Vector(6);
	Vector* vp = new Vector(7);
	Vector a(v);

	Vector w = v2;



	cout << v[3]; // Oczekujemy 0.
	v[3] = 7;
	cout << v[3]; // Oczekujemy 7;

	v2 = v;
	cout << v2[3];


	try {

	}
	catch (std::exception e) {
		cerr << e.what << endl;
	}
	catch (...) {
		cerr << "Nie wiem co sie dzieje" << endl;
	}

	cout << endl;

	return 0;
}
