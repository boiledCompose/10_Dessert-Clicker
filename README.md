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

<h3>액티비티 간 이동</h3>

사용자가 액티비티에서 벗어났다고 완전히 닫히는 것은 아니다.
  
  
</p>

