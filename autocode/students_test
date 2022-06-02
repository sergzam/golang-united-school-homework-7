package coverage

import (
	"fmt"
	"os"
	"reflect"
	"testing"
	"time"
)

// DO NOT EDIT THIS FUNCTION
func init() {
	content, err := os.ReadFile("students_test.go")
	if err != nil {
		panic(err)
	}
	err = os.WriteFile("autocode/students_test", content, 0644)
	if err != nil {
		panic(err)
	}
}

// WRITE YOUR CODE BELOW

func TestPeople_Len(t *testing.T) {
	people := People{
		{
			firstName: "First",
			lastName:  "First",
			birthDay:  time.Now(),
		},
		{
			firstName: "Second",
			lastName:  "Second",
			birthDay:  time.Now(),
		},
	}

	t.Run("", func(t *testing.T) {
		l := people.Len()
		if l != len(people) {
			t.Logf("length is not okay: people lenght is: %d and people's method length is: %d", len(people), l)
			t.Fail()
		}
	})
}

func TestPeople_Less(t *testing.T) {
	people := People{
		{
			firstName: "First",
			lastName:  "First",
			birthDay:  time.Now(),
		},
		{
			firstName: "First",
			lastName:  "First",
			birthDay:  time.Now(),
		},
		{
			firstName: "Second",
			lastName:  "Second",
			birthDay:  time.Now(),
		},
		{
			firstName: "Second",
			lastName:  "Second",
			birthDay:  time.Now().Add(time.Minute * 10),
		},
		{
			firstName: "Third",
			lastName:  "Third",
			birthDay:  time.Now(),
		},
		{
			firstName: "Forth",
			lastName:  "Forth",
			birthDay:  time.Now(),
		},
	}

	testsCases := []struct {
		i      int
		j      int
		result bool
		title  string
	}{
		{
			i:     0,
			j:     1,
			title: "the first test",
		},
		{
			i:     2,
			j:     1,
			title: "the second test",
		},
		{
			i:     0,
			j:     0,
			title: "the third test",
		},
		{
			i:     2,
			j:     3,
			title: "the forth test",
		},
	}

	for _, testsCase := range testsCases {
		t.Run(testsCase.title, func(t *testing.T) {
			if r := people.Less(testsCase.i, testsCase.j); r != testsCase.result {
				t.Logf("result wrong: r is %t and testsCase was: %t", r, testsCase.result)
				t.Fail()
			}
		})
	}
}

func TestPeople_Swap(t *testing.T) {
	people := People{
		{
			firstName: "First",
			lastName:  "First",
			birthDay:  time.Now(),
		},
		{
			firstName: "First",
			lastName:  "First",
			birthDay:  time.Now(),
		},
		{
			firstName: "Second",
			lastName:  "Second",
			birthDay:  time.Now(),
		},
		{
			firstName: "Second",
			lastName:  "Second",
			birthDay:  time.Now().Add(time.Minute * 10),
		},
		{
			firstName: "Third",
			lastName:  "Third",
			birthDay:  time.Now(),
		},
		{
			firstName: "Forth",
			lastName:  "Forth",
			birthDay:  time.Now(),
		},
	}

	testsCases := []struct {
		i     int
		j     int
		title string
	}{
		{
			i:     1,
			j:     2,
			title: "the first test",
		},
		{
			i:     0,
			j:     3,
			title: "the second test",
		},
	}

	for _, testsCase := range testsCases {
		t.Run(testsCase.title, func(t *testing.T) {
			personI := people[testsCase.i]
			personJ := people[testsCase.j]
			people.Swap(testsCase.i, testsCase.j)
			if people[testsCase.i] != personJ || people[testsCase.j] != personI {
				t.Logf(
					"swap went wrong: personJ is %v, people I is %v | personI is %v, people J is %v",
					personJ, people[testsCase.i], personI, people[testsCase.j],
				)
				t.Fail()
			}
		})
	}
}

func TestNew(t *testing.T) {
	testsCases := []struct {
		input  string
		result *Matrix
		err    error
		title  string
	}{
		{
			input: "12\n14 16",
			err:   fmt.Errorf("Rows need to be the same length"),
			title: "the first case",
		},
		{
			input: "12\n14 \n A",
			err:   fmt.Errorf("strconv.Atoi: parsing \"A\": invalid syntax"),
			title: "the second case",
		},
		{
			input:  "12 11\n14 16",
			result: &Matrix{rows: 2, cols: 2, data: []int{12, 11, 14, 16}},
			title:  "the third case",
		},
	}

	for _, testsCase := range testsCases {
		t.Run(testsCase.title, func(t *testing.T) {
			matrix, err := New(testsCase.input)
			if err != nil && err.Error() != testsCase.err.Error() {
				t.Logf("wrong error: %v, expected: %v", err, testsCase.err)
				t.Fail()
			}
			if matrix != nil && testsCase.result != nil && !reflect.DeepEqual(*matrix, *testsCase.result) {
				t.Logf("wrong matrix: %v, expected: %v", matrix, testsCase.result)
				t.Fail()
			}
		})
	}
}

func TestMatrix_Rows(t *testing.T) {
	expected := [][]int{{12, 11}, {14, 16}}
	matrix := Matrix{rows: 2, cols: 2, data: []int{12, 11, 14, 16}}
	t.Run("rows test", func(t *testing.T) {
		if !reflect.DeepEqual(matrix.Rows(), expected) {
			t.Logf("wrong rows: %v, expected: %v", matrix.Rows(), expected)
			t.Fail()
		}
	})
}

func TestMatrix_Cols(t *testing.T) {
	expected := [][]int{{12, 14}, {11, 16}}
	matrix := Matrix{rows: 2, cols: 2, data: []int{12, 11, 14, 16}}
	t.Run("cols test", func(t *testing.T) {
		if !reflect.DeepEqual(matrix.Cols(), expected) {
			t.Logf("wrong cols: %v, expected: %v", matrix.Cols(), expected)
			t.Fail()
		}
	})
}

func TestMatrix_Set(t *testing.T) {
	matrix := Matrix{rows: 3, cols: 3, data: []int{12, 11, 14, 16, 1, 17, 27, 75, 23, 2}}
	testsCases := []struct {
		row, col, value int
		result          bool
		title           string
	}{
		{
			row:    4,
			col:    4,
			result: false,
			title:  "the first test",
		},
		{
			row:    2,
			col:    2,
			value:  15,
			result: true,
			title:  "the second test",
		},
	}

	for _, testsCase := range testsCases {
		t.Run(testsCase.title, func(t *testing.T) {
			result := matrix.Set(testsCase.row, testsCase.col, testsCase.value)
			if result != testsCase.result || (len(matrix.data) > testsCase.row*matrix.cols+testsCase.col && matrix.data[testsCase.row*matrix.cols+testsCase.col] != testsCase.value) {
				t.Logf("wrong set attemp result: %v, expected: %v", result, testsCase.result)
				t.Logf("wrong set attemp data: %v, expected: %v", matrix.data[testsCase.row*matrix.cols+testsCase.col], testsCase.value)
				t.Fail()
			}
		})
	}
}
