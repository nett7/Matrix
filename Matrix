#pragma once
#define _CRT_SECURE_NO_WARNINGS

#include <iostream>
#include <initializer_list>
#include <exception>
#include <stdexcept>


using namespace std;

template<typename type, size_t Rows, size_t Columns>
class Matrix {
private:
	type * *ptr;
public:


	Matrix() : ptr(nullptr) {};

	Matrix(initializer_list<type> list);

	Matrix(const Matrix &mat);

	void swap(Matrix &mat);

	Matrix &operator=(const Matrix &mat);

	bool empty() const;

	size_t columns();

	size_t rows();

	Matrix operator-(const Matrix &) const;

	Matrix operator+(const Matrix &) const;

	type *operator[](size_t index);

	bool operator==(const Matrix &) const;

	template<class T, size_t R, size_t C> friend ostream &operator<<(ostream &, const Matrix<T, R, C> &);

	template<class T1, size_t R1, size_t C1>
	friend istream &operator>>(istream &, Matrix<T1, R1, C1> &);

	~Matrix();


};

template<class type, size_t Rows, size_t Columns>
Matrix<type, Rows, Columns>::~Matrix() {
	for (size_t i = 0; i < Rows; i++) {
		delete[] ptr[i];
	}
	delete[] ptr;
}

template<class type, size_t Rows, size_t Columns>
bool Matrix<type, Rows, Columns>::empty() const {
	return (ptr ==nullptr);
}

template<class type, size_t Rows, size_t Columns>
size_t Matrix<type, Rows, Columns>::columns() {
	return Columns;
}
template<class type, size_t Rows, size_t Columns>
size_t Matrix<type, Rows, Columns>::rows() {
	return Rows;
}

template<class type, size_t Rows, size_t Columns>
Matrix<type, Rows, Columns> Matrix<type, Rows, Columns>::operator-(const Matrix<type, Rows, Columns> &mat) const {
	Matrix<type, Rows, Columns> temp(*this);
	for (size_t x = 0; x < Rows; x++) {
		for (size_t y = 0; y < Columns; y++) {
			temp[x][y] -= mat.ptr[x][y];
		}
	}
	return Matrix(temp);
}


template<class type, size_t Rows, size_t Columns>
type *Matrix<type, Rows, Columns>::operator[](size_t index) {
	return ptr[index];
};


template<class type, size_t Rows, size_t Columns>
void Matrix<type, Rows, Columns>::swap(Matrix &mat) {
	std::swap(ptr, mat.ptr);
}

template<class type, size_t Rows, size_t Columns>
Matrix<type, Rows, Columns> Matrix<type, Rows, Columns>::operator+(const Matrix &mat) const {
		Matrix temp(*this);
		for (size_t x = 0; x < Rows; x++) {
			for (size_t y = 0; y < Columns; y++) {
				temp[x][y] += mat.ptr[x][y];
			}
		}

	return Matrix(temp);
}

template<class type, size_t Rows, size_t Columns>
bool Matrix<type, Rows, Columns>::operator==(const Matrix &mat) const {
	for (size_t x = 0; x < Rows; x++)
		for (size_t y = 0; y < Columns; y++)
			if (ptr[x][y] != mat.ptr[x][y])
				return false;
	return true;


}

template<class type, size_t Ro, size_t Col>
ostream &operator<<(ostream &os, const Matrix<type, Ro, Col> &mat) {
	if (mat.empty()) {
		os << "There is no elements\n";
		return os;
	}
	else
	{
		for (size_t x = 0; x < Ro; x++) {
			for (size_t y = 0; y < Col; y++)
				os << mat.ptr[x][y] << " ";
			os << endl;
		}
		return os;
	}
}

template<class type, size_t Rows, size_t Columns>
istream &operator>>(istream &is, Matrix<type, Rows, Columns> &mat) {
	if (is) {
		mat.ptr = new type *[Rows];
		for (size_t i = 0; i < Rows; i++) {
			mat.ptr[i] = new type[Columns];
		}
		for (size_t i = 0; i < Rows; i++) {
			for (size_t j = 0; j < Columns; j++) {
				is >> mat.ptr[i][j];
			}
		}
	}
	else cout << "Cant open the file!!!\n";
	return is;


}

template<class type, size_t Rows, size_t Columns>
Matrix<type, Rows, Columns>::Matrix(initializer_list<type> list) {
	size_t k = 0;
	if (Rows * Columns < list.size()) {
		throw length_error("Not correct size");
	}
	ptr = new type *[Rows];
	for (size_t i = 0; i < Rows; i++) 
		ptr[i] = new type[Columns];

	if (Rows*Columns > list.size()) {
		for (size_t i = 0; i < Rows; i++)
			for (size_t j = 0; j < Columns; j++)
				ptr[i][j] = 0;
	}
	

	auto iter = list.begin();
	for (size_t i = 0; i < Rows; i++) {
		for (size_t j = 0; j < Columns; j++) {
			if (k > list.size() - 1)
				break;
			ptr[i][j] = *iter;
			iter++;
			k++;
		}
		if (k > list.size() - 1)
			break;
	}
}

template<class type, size_t Rows, size_t Columns>
Matrix<type, Rows, Columns>::Matrix(const Matrix<type, Rows, Columns> &mat) {
	ptr = new type *[Rows];
	for (size_t i = 0; i < Rows; i++) {
		ptr[i] = new type[Columns];
		copy(&mat.ptr[i][0], &mat.ptr[i][Columns], &ptr[i][0]);
	}

}

template<typename type, size_t Rows, size_t Columns>
Matrix<type, Rows, Columns> &Matrix<type, Rows, Columns>::operator=(const Matrix &mat) {
	if (this == &mat)
		return *this;
	else {
		if (ptr != nullptr) {
			for (size_t i = 0; i < Rows; i++) {
				delete[] ptr[i];
			}
			delete[] ptr;
		}

			ptr = new type *[Rows];
			for (size_t i = 0; i < Rows; i++) {
				ptr[i] = new type[Columns];
				copy(&mat.ptr[i][0], &mat.ptr[i][Columns], &ptr[i][0]);
			}
			return *this;
		}
}

