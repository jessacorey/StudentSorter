// Student.java
class Student {
    int rollno;
    String name;
    String address;
// Constructor 

    public Student(int rollno, String name, String address) {
        this.rollno = rollno;
        this.name = name;
        this.address = address;
    }
}

// RollNoComparator.java
import java.util.Comparator;

//Compares students based on roll number 
class RollNoComparator implements Comparator<Student> {
    @Override
    public int compare(Student s1, Student s2) {
        return Integer.compare(s1.rollno, s2.rollno);
    }
}

// MergeSort.java
import java.util.ArrayList;
import java.util.Comparator;

// Implementing the merge sort algorithm for sorting Students 
class MergeSort {
    public static void mergeSort(ArrayList<Student> students, Comparator<Student> comparator) {
        int size = students.size();
        if (size < 2) {
            return;
        }

        int mid = size / 2;
// Divides list into two halves 

        ArrayList<Student> left = new ArrayList<>(students.subList(0, mid));
        ArrayList<Student> right = new ArrayList<>(students.subList(mid, size));
// Sort the left and right halves 

        mergeSort(left, comparator);
        mergeSort(right, comparator);

// Merge the sorted halves 

        merge(students, left, right, comparator);
    }

// Method to merge two sorted lists 
    private static void merge(
            ArrayList<Student> students,
            ArrayList<Student> left,
            ArrayList<Student> right,
            Comparator<Student> comparator) {
        int leftSize = left.size();
        int rightSize = right.size();
        int i = 0, j = 0, k = 0;
// Merge the two lists while keeping the order

        while (i < leftSize && j < rightSize) {
            if (comparator.compare(left.get(i), right.get(j)) < 0) {
                students.set(k++, left.get(i++));
            } else {
                students.set(k++, right.get(j++));
            }
        }

// Copy any remaining elements from left and right lists 
        while (i < leftSize) {
            students.set(k++, left.get(i++));
        }

        while (j < rightSize) {
            students.set(k++, right.get(j++));
        }
    }
}

// StudentSorter.java
import java.util.ArrayList;

// Main class for sorting students based on roll numbers 
public class StudentSorter {

// Creating the lists of studenst with random data 
    public static void main(String[] args) {
        ArrayList<Student> students = new ArrayList<>();
        students.add(new Student(3, "R2D2", "Tatooine"));
        students.add(new Student(10, "Han Solo", "Corellia"));
        students.add(new Student(5, "Leia Organa", "Alderaan"));
        students.add(new Student(1, "Obi-Wan Kenobi", "Stewjon"));
        students.add(new Student(4, "Yoda", "Dagobah"));
        students.add(new Student(7, "Chewbacca", "Kashyyyk"));
        students.add(new Student(8, "Padmé Amidala", "Naboo"));
        students.add(new Student(9, "Darth Maul", "Haruun Kal"));
        students.add(new Student(2, "Ahsoka Tano", "Coruscant"));
        students.add(new Student(6, "Anakin Skywalker", "Jakku"));

        // Sorting students by roll number using merge sort
        MergeSort.mergeSort(students, new RollNoComparator());

        // Displaying sorted students
        for (Student student : students) {
            System.out.println("Roll No: " + student.rollno + ", Name: " + student.name + ", Address: " + student.address);
        }
    }
}

