# ArrayUtilities
package sysImplementation;

public class Utilities {
	public Utilities() {

	}

	public static java.lang.String getArrayString(int[] array, char separator) {
		// checks for if array is null
		if (array == null) {
			throw new java.lang.IllegalArgumentException("Array is null");
		}
		// checks for if array is empty
		if (array.length == 0) {
			return "";
		}
		StringBuilder hold = new StringBuilder();
		for (int i = 0; i < array.length; i++) {
			// adds all elements of array to the stringbuilder array
			hold.append(array[i]);
			// for every element except the last add separator after
			if (i != array.length - 1) {
				hold.append(separator);
			}
		}
		return hold.toString();
	}

	public static int getInstances(int[] array, int lowerLimit, int upperLimit) {
		// checks for if array is null
		if (array == null) {
			throw new java.lang.IllegalArgumentException("Array is null");
		}
		int counter = 0;
		for (int i = 0; i < array.length; i++) {
			// adds to the counter if an element is between the bound set
			if (array[i] >= lowerLimit && array[i] <= upperLimit) {
				counter += 1;
			}
		}
		return counter;
	}

	public static int[] filter(int[] array, int lowerLimit, int upperLimit) {
		// checks criteria to make sure that array is not null and limits are valid
		if (array == null || lowerLimit > upperLimit) {
			throw new java.lang.IllegalArgumentException("Array is null or UpperLimit is less than LowerLimit");
		}
		// initializes an array with the number of elements that are valid given
		// parameters
		int[] hold = new int[getInstances(array, lowerLimit, upperLimit)];
		int counter = 0;
		for (int i = 0; i < array.length; i++) {
			// adds the valid element to the array after checking parameter once more
			if (array[i] >= lowerLimit && array[i] <= upperLimit) {
					hold[counter] = array[i];
					counter++;
			}
		}
		return hold;
	}

	public static void rotate(int[] array, boolean leftRotation, int positions) {
		// checks for if the array is null
		if (array == null) {
			throw new java.lang.IllegalArgumentException("Array is null");
		}
		// checks for if the array is valid
		if (array.length < 2) {
			return;
		}
		positions = positions % array.length;
		// based on if parameter is true or false the array is shifted right or left
		if (leftRotation) {
			rotateLeft(array, positions);
		} else {
			rotateRight(array, positions);
		}
	}

	private static void rotateRight(int[] holdR, int holdRightPositions) {
		// reverse first part of array
		reverse(holdR, 0, holdR.length - holdRightPositions - 1);
		// reverse second part of array
		reverse(holdR, holdR.length - holdRightPositions, holdR.length - 1);
		// reverse entire array
		reverse(holdR, 0, holdR.length - 1);
	}

	private static void rotateLeft(int[] holdL, int holdLeftPositions) {
		// reverse first part of array
		reverse(holdL, 0, holdLeftPositions - 1);
		// reverse second part of array
		reverse(holdL, holdLeftPositions, holdL.length - 1);
		// reverse entire array
		reverse(holdL, 0, holdL.length - 1);
	}

	private static void reverse(int[] array, int start, int end) {
		// checks to make sure that the parameter for comparison is valid and exchanges
		// values
		while (start < end) {
			int hold = array[start];
			array[start] = array[end];
			array[end] = hold;
			start++;
			end--;
		}
	}

	public static java.lang.StringBuffer[] getArrayStringsLongerThan(java.lang.StringBuffer[] array, int length) {
		// checks to see if array is null
		if (array == null) {
			throw new java.lang.IllegalArgumentException("Array is null");
		}
		int counter = 0;
		// counts elements that are in the array with required length parameter
		for (int i = 0; i < array.length; i++) {
			if (array[i].length() > length) {
				counter += 1;
			}
		}
		// returns null copy if no such elements are found
		if (counter == 0) {
			return new StringBuffer[0];
		}
		// adds the desired elements into a new array by traversing through the original
		// one
		else {
			int sample = 0;
			StringBuffer[] hold = new StringBuffer[counter];
			for (int j = 0; j < array.length; j++) {
				if (array[j].length() > length) {
						hold[sample] = array[j];
						sample ++;
				}
			}
			return hold;
		}
	}

}
