## 기본 메서드 정리



### GetComponent<T>();
T에 맞는 컴포넌트를 가져옵니다.

```C#
private Rigidbody playerRigidbody;

void Start()
{
    playerRigidbody = GetComponent<Rigidbody>();
}
```


### [SerializeField]
직렬화를 합니다. 기본적으로 인스펙터에서  public으로 설정하면 해당 컴포넌트를 설정할 수 있는데 하지만 이는 외부 스크립트에서도 해당 컴포넌트에 접근할 수 있습니다. 외부 스크립트에선 접근이 불가하고 인스펙터에선 접근이 가능하게 하기 위해서 사용합니다.

```C#
public float speed = 8f;             // 해당 speed는 public으로 인스펙터와 외부 스크립트에서도 접근 가능합니다.
                                                
[SerializeField]                     // 해당 Rigidbody 는 인스펙터에선 접근 가능하지만 외부 스크립트에서 접근         
private Rigidbody playerRigidbody;   // 불가능합니다. 기본적으로 private 이기 떄문에 해당 클래스가 아니면 접근 불가능합니다. 
                                      // 기본 언어 private과 동일
```


### Input 
Input.GetKey()는 키코드를 매개변수로 넘겨주면 그게 맞는 bool값을 반환합니다.
키코드는 유니티에서 제공하는 Keycode enumclass 입니다.
```C#
if(Input.GetKey(KeyCode.UpArrow) == true)
```

+ Input.GetKey() : 해당 키를 **누르는 동안** true. 그 외에는 false 반환
+ Input.GetKeyDown() : 해당 키를 **누르는 순간** true. 그 외에는 false 반환
+ Input.GetKeyUp() : 해당 키를 누르다가 손을 **떼는 순간** true. 그 외에는 false 반환

#### Input.GetAxis() 메서드
GetAxis 메서드는 매개변수로 String Axis 를 받습니다.

```C#
float xInput = Input.GetAxis("Horizontal");
```

Horizontal 축의 경우 수평 축에 대응되는 키가 입력되면 그에 맞는 출력값을 반환합니다.
+ A키 혹은 왼쪽 방향키   : -1.0
+ D키 혹은 오른쪽 방향키 : +1.0
+ W키 혹은 위쪽 방향키   : +1.0
+ S키 혹은 아래쪽 방향키 : -1.0
+ 아무것도 누르지 않음   :  0
이 때 반환값은 float 타입으로 반환됩니다. 예제를 살펴보면

```C#
float xInput = Input.GetAxis("Horizontal");
float xSpeed = xInput * speed;
```
A D 혹은 오른쪽 왼쪽 방향키가 입력되면 그 값에 speed를 곱해줍니다. 누를 때마다 xSpeed의 값이 변경됩니다.
