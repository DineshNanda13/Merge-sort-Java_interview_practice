# Merge-sort-Java_interview_practice
package com.mergeSort;

/**
 *
 * @author Dinesh Nanda
 */

//O(n log n) // efficient for large data sets not much for small

public class MergeSort {

    private static void printArray(int[] array) {
        for (int i : array) {
            System.out.print(i + " ");
        }
        System.out.println();
    }

    private static int[] mergeSort(int[] array) {

        if (array.length <= 1) {
            return array;
        }

        int midpoint = array.length / 2;

        int[] left = new int[midpoint];
        int[] right;

        if (array.length % 2 == 0) {
            right = new int[midpoint];
        } else {
            right = new int[midpoint + 1];
        }
        //populate left array
        for (int i = 0; i < midpoint; i++) {
            left[i] = array[i];
        }
        //populate right array
        for (int j = 0; j < right.length; j++) {
            right[j] = array[midpoint + j];
        }

        int[] result = new int[array.length];

        left = mergeSort(left);
        right = mergeSort(right);

        result = merge(left, right);

        return result;
    }

    //merge left & right sorted arrays
    private static int[] merge(int[] left, int[] right) {

        int[] result = new int[left.length + right.length];

        int leftPointer, rightPointer, resultPointer;
        leftPointer = rightPointer = resultPointer = 0;

        while (leftPointer < left.length || rightPointer < right.length) {

            if (leftPointer < left.length && rightPointer < right.length) {

                if (left[leftPointer] < right[rightPointer]) {

                    result[resultPointer] = left[leftPointer];
                    resultPointer++;
                    leftPointer++;

                } else {
                    result[resultPointer++] = right[rightPointer++];
                }
            } //if elements are only in left array
            else if (leftPointer < left.length) {
                result[resultPointer++] = left[leftPointer++];
            } //if elements are only in right array
            else if (rightPointer < right.length) {
                result[resultPointer++] = right[rightPointer++];
            }
        }
        return result;
    }

    public static void main(String[] args) {

        int[] array = {3, 2, 6, 9, 1};

        array = mergeSort(array);
        System.out.println("Sorted Array: ");
        printArray(array);
    }

}

