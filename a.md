2018-12-28일 수업내용 정리
==================================
접근자
-----
* public
  * 적용 대상: 필드 메소드 생성자
  * 접근 제한: 없음
* protected (주로 상속에서 많이씀)
  * 적용 대상:필드 메소드 생성자
  * 접근 제한: 같은 패키지의 클래스 또는 자식 클래스 이외의 클래스
* private
  * 적용 대상:필드,메소드,생성자
  * 접근 제한: 모든 외부 클래스(내부 전용)
* default(왠만하면 접근 지시자 꼭 붙여야함)
  * 같은 패키지 이외의 클래스
------------------------------
static 클래스 변수
-------

* 클래스 이름으로 접근가능

<br/>
Class A{<br/>
  static int a; //클래스변수<br/>
  int b;       //인스턴스 변수<br/>
...<br/>
  public void swap(){<br/>
    int c; //지역 변수<br/>
  }<br/>
}
<br/>
Class Main{<br/>
  public void main()
  {<br/>
    A.a=10; //가능<br/>
  }<br/>
}
<br/>

* new 를 통해 생성된 변수(인스턴스 변수)
  * heap에 저장
* 매소드 안의 변수(지역변수)
  * 변수 선언문이 수행될대 생성
  * stack 에 저장
* 클래스 변수
  * 클래스가 메모리에 올라갈때 생성됨
  * method area에 저장
![Alt text](/스케치.png)


----------------------------------------------
자바에서는 객체를 사용하여 C언어 포인터 변경을 한다.<br>

public class StaticMethod {<br>
	private int n;<br>
	public static int m;<br>

	public int getN() {
		return n;
	}
	public void setN(int n) {
		this.n = n;
	}
	public static int getM() {
		return m;
	}
	public static void setM(int m) {
		StaticMethod.m = m;
	}
	public void f1()
	{
		n=10;


		//원칙적으로는 클래스이름(네임스페이스) 로 접근해야함
		//하지만 같은 클래스인 경우에는 생략가능하다.
		//StaticMethod.m = 20;
		m=20;
	}
	public static void f2()
	{
		//error
		//n=10;
		m=30;
	}
	public void f3()
	{
		f1();
		f2();
	}
	public static void f4()
	{
		//error
		//f1();
		f2();
	}
	public static void main(String[] args)
	{
		f2();
		f4();
    //f1(),f3(); error
	}
}
<hr>

리펙토링
-------
public void show() <br>
	{<br>
		System.out.println("점[x="+x+", y="+y+"]을 그렸습니다");<br>
	}<br><br><br>
	public void show(boolean visible)<br>
	{<br>	if(visible)<br>
		{<br>
			show(); **//리펙토링 방식 이렇게 하면 유지보수가 좋다.**
      <br>
		}<br>
		else<br>
			System.out.println("점[x="+x+", y="+y+"]을 지웠습니다.");<br>
	}<br>
