열거형의 순서를 비교

순서가 더 앞에 있으면 -1
같으면 0
뒤에 있으면 1

ex)
enum Level {A, B, C;}

l1 = Level.A, l2 = Level.B. l3 = Level.C
l1.compareTo(l2) => -1
l3.compareTo(l2) => 1
l1.compareTo(l1) => 0