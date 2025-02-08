# Leetcode---2349
Design a Number Container System
//code in java
import java.util.*;

class NumberContainers {
    private Map<Integer, Integer> indexToNumber;
    private Map<Integer, TreeSet<Integer>> numberToIndices;

    public NumberContainers() {
        indexToNumber = new HashMap<>();
        numberToIndices = new HashMap<>();
    }

    public void change(int index, int number) {
        if (indexToNumber.containsKey(index)) {
            int originalNumber = indexToNumber.get(index);
            numberToIndices.get(originalNumber).remove(index);
            if (numberToIndices.get(originalNumber).isEmpty()) {
                numberToIndices.remove(originalNumber);
            }
        }
        indexToNumber.put(index, number);
        numberToIndices.computeIfAbsent(number, k -> new TreeSet<>()).add(index);
    }

    public int find(int number) {
        if (!numberToIndices.containsKey(number)) {
            return -1;
        }
        return numberToIndices.get(number).first();
    }
}
