#설치 실패
 APK 설치 실패, LogCat Log에 INSTALL_FAILED_TEST_ONLY, install failed -15 확인 
 gradle.properties에 android.injected.testOnly=false 설정, manifest.xml에 android:testOnly=false로 값을 설정하였으나 
 apk 생성하면 AndrodiManifest.xml의 android:testOnly 값이 강제로 true로 설정되는 문제 확인
 원인은 compileSdkPreview = "UpsideDownCake" 설정 시 testOnly값이 강제로 설정되는것으로 보임
 해당 코드 제거 후 정상 설치 확인

 동일한 케이스 stackoverflow
 https://stackoverflow.com/questions/75844075/app-not-installed-error-when-trying-to-install-signed-apk-on-android-device

 
