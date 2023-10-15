# 기능
말 그대로 비어있는 List를 리턴한다.
Collections 내부의 private class 인 EmptyList()를 싱글톤 패턴으로 리턴한다.
final 변수이고 immutable 하다.

# 용도
일단 immutable 하기 때문에, 초기화 할 때 사용하는 녀석은 아니다.
만약 비어있는 List를 리턴해야할 때, 이녀석을 리턴해주면, 메모리를 아낄 수 있기 때문에 존재한다고 한다.
