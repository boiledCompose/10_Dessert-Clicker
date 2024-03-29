<p>
<h2>안드로이드 생명주기</h2>  
<p align="center"> <img src="https://developer.android.com/static/codelabs/basic-android-kotlin-compose-activity-lifecycle/img/468988518c270b38_856.png?hl=ko" width="500" height="500"/></p>
    
<h3>onCreate()</h3>

`onCreate()` 메서드는모든 액티비티에서 구현해야 하는 메서드이다. 이 메서드에서 액티비티의 초기화가 실행된다. 예를 들어 `onCreate()`에서 액티비티의 UI 레이아웃을 지정하는 `setContent()`를 호출한다.

`onCreate()`가 실행되면 액티비티가 생성됨으로 간주된다.

<br>

<h3>onStart()</h3>

`onStart()` 메서드는 `onCreate()` 직후에 호출된다. 이 메서드를 통해 액티비티가 화면에 표시된다.

활동을 초기화하는 데 한 번만 호출되는 `onCreate`와 달리 `onStart`는 시스템에서 활동의 수명 주기 동안 여러 번 호출할 수 있다.

`onStart`는 `onStop()`과 대응된다. 사용자가 앱을 시작한 후 기기 홈 화면으로 돌아오거나 다른 앱으로 전환하면 활동이 중지되는 의미의 `onStop()` 메서드가 불리고 더 이상 화면에 표시되지 않는다.

>[!NOTE]
> `onRestart()` 메서드는 `onCreate()`와 `onStart()` 메서드 사이에 호출되는 것이 아니고, `onStop()` 상태에서 `onStart()`로 전환되는 경우에 그 중간에 호출되는 메서드이다.

<br>

<h3>onResume()</h3>

`onResume()` 메서드는 앱을 포그라운드로 가져오고 사용자와 앱 간 상호작용을 가능하도록 한다. 이 메서드는 다시 시작할 대상이 없어도 시작 시 호출된다.

<br>

<h2>수명 주기 사용 사례</h2>

<h3>1. 액티비티 열기 및 닫기</h3>

- 액티비티가 처음 시작되면 `onCreate()` > `onStart()' > `onResume()` 순으로 콜백이 호출된다.
  
- 기기에서 뒤로 가기 버튼을 누르거나 사용자가 `finish()`를 통해 수동으로 액티비티를 끝낼 수 있다. 또한 사용자가 앱을 강제 종료할 수도 있다. 이러한 경우 `onPause()` > `onStop()` 순으로 콜백이 호출된다.

- 최종적으로 앱이 종료되는 경우 'onStop()` 이후에 `onDestroy()' 콜백이 호출된다.

<br>

<h3>2. 액티비티 간 이동</h3>

사용자가 액티비티에서 벗어났다고 완전히 닫히는 것은 아니다.
    - 액티비티는 백그라운드에 배치된다. 이와 반대의 경우는 포그라운드에 있거나 화면에 표시되는 경우다.
    - 사용자가 앱으로 돌아오면 벗어나기 전 액티비티가 다시 시작되어 화면에 표시된다. 
  
앱 실행 중 사용자가 홈 버튼을 누르면 앱이 완전히 종료되는 대신 백그라운드로 전환된다. 이때 `onPause()`와 `onStop()` 메서드가 호출된다.
    - `onPause()`가 호출되면 앱에 더 이상 포커스가 없어진다.
    - `onStop()`이 호출되면 앱이 더 이상 화면에 표시되지 않는다.

앱으로 돌아가게 되면 `onRestart()` 및 `onStart()`로 다시 시작된 후 `onResume()`으로 재개된다.

>[!NOTE]
> 포그라운드로 돌아오는 액티비티에 대해서 `onCreate()`가 아닌 `onRestart()`가 호출되는 것을 명심하자. `onCreate()`는 액티비티가 처음 실행될 때 한 번 호출되며, 액티비티가 완전히 종료되기 전까진 다시 호출되지 않는다.   
> `onStart()`와 `onStop()`은 사용자가 액티비티에서 나가거나 액티비티로 이동할 때 여러 번 호출된다.

<br>

<h3>3. 부분적으로 액티비티 숨기기</h3>

앱이 시작되고 `onStart`가 호출되면 앱이 화면에 표시되고, `onResume()`이 호출되면 앱은 사용자의 포커스를 획득한다.

앱이 백그라운드로 이동하면 `onPause()`를 통해 포커스를 잃고, `onStop()`을 통해 앱이 화면에 표시되지 않는다.

앱이 화면에서 완전히 사라지지 않았지만 포커스만 잃는 경우도 있을 수 있다. 

예를 들면 공유 화면은 전체 화면의 절반 정도만 차지하는 화면으로 나머지 화면엔 기존 액티비티가 포커스를 잃은 채로 표시된다. 이런 경우 `onPause()`만 호출되고 `onStop`은 호출되지 않는다.

>[!IMPORTANT]
> `onPause()`만 사용한 중단은 보통 활동으로 돌아가거나 다른 활동 또는 앱으로 이동하기 전에 잠시 지속된다. 일반적으로 UI를 계속 업데이트하여 나머지 앱이 멈춘 것처엄 보이지 않도록 하는 것이 좋다.

<br>

<h2>구성 변경사항 살펴보기</h2>

***구성 변경***은 기기의 상태가 매우 급격하게 변경되어 시스템이 변경 사항을 확인하기 위해 활동을 완전히 종료하고 다시 빌드하면서 발생한다.   
    
1. 사용자가 기기 언어를 변경하여 다른 텍스트 방향과 문자열 길이를 수용하도록 전체 레이아웃을 변경해야 할 수 있다.
2. 사용자가 기기를 토크에 연결하거나 물리적 키보드를 추가하면 앱 레이아웃은 다른 디스플레이 크기나 레이아웃을 활용해야 할 수 있다.
3. 기기 방향이 변경되어 새 방향에 맞게 레이아웃을 변경해야 할 수 있다.

<br>

<h3>구성 변경으로 인한 onDestroy() 호출</h3>

구성 변경이 발생하면 앱이 완전히 종료된다. 이때 `onPause()`와 `onStop()`에 이어 `onDestroy()`까지 호출된다.   

<br>

<h3>구성 변경으로 인한 데이터 손실</h3>

화면 회전을 할 경우, 액티비티가 완전히 종료되었다가 다시 초기화되면서 모든 데이터들이 기본값으로 초기화된다.   

이러한 상황을 방지하기 위해 컴포저블의 수명 주기와 그 상태를 관찰하고 유지하는 방법을 알아야 한다.

<br>

<h3>컴포저블의 수명 주기</h3>

`Composable` 함수에는 액티비티의 수명 주기와 별개인 자체 수명 주기가 존재한다. **수명 주기는 컴포지션을 시작하고 0회 이상 재구성한 다음 컴포지션을 종료하는 이벤트**로 구성된다.

1. 앱의 UI는 처음에 `Composition`이라는 프로세스에서 `Composable` 함수를 실행하여 빌드된다.
2. 앱 상태가 변경되면 `Recomposition`이 예약된다. `Recomposition`은 상태가 변경되었을 수 있는 `Composable` 함수를 Compose에서 다시 실행하고 업데이트된 UI를 만드는 것을 의미한다. `Composition`은 이러한 변경사항을 반영하도록 업데이트된다.

Compose에서 상태가 변하는 객체를 나타내기 위해서 `State` 또는 `MutableState`를 사용한다.
```
    var revenue = mutableStateOf(0)
```

`Recomposition` 중에 값을 유지하고 재사용하기 위해 `remember` API를 사용한다.
```
    var  revenue by remember { mutableStateOf(0) }
```

하지만 `remember`는 구성 변경 중에 상태 유지를 지원하지 않는다. Compose가 구성 변경 중에 상태를 유지하려면 `rememberSaveable`를 사용해야 한다.

<br>

<h3>rememberSaveable을 사용하여 구성 변경 시 값 저장</h3>

`rememberSaveable`은 리컴포지션 및 구성 변경 중 값을 저장하는 기능을 제공한다.

```
var revenue by rememberSaveable { mutableStateOf(0) }
...
var currentDessertImageId by rememberSaveable {
    mutableStateOf(desserts[currentDessertIndex].imageId)
}
```
화면을 바꾸면 값들이 초기화되던 이전 상황과는 달리 `rememberSaveable`로 저장하는 값들은 초기화되지 않고 값을 유지하게 된다.

</p>

