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
</p>
