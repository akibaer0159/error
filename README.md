#설치 실패
 APK 설치 실패, LogCat Log에 INSTALL_FAILED_TEST_ONLY, install failed -15 확인 
 gradle.properties에 android.injected.testOnly=false 설정, manifest.xml에 android:testOnly=false로 값을 설정하였으나 
 apk 생성하면 AndrodiManifest.xml의 android:testOnly 값이 강제로 true로 설정되는 문제 확인
 원인은 compileSdkPreview = "UpsideDownCake" 설정 시 testOnly값이 강제로 설정되는것으로 보임
 해당 코드 제거 후 정상 설치 확인

 동일한 케이스 stackoverflow
 https://stackoverflow.com/questions/75844075/app-not-installed-error-when-trying-to-install-signed-apk-on-android-device


 #BottomSheetDialogFragment FullScreen

    override fun onStart() {
        super.onStart()
        setupRatio(dialog as BottomSheetDialog)
    }

    private fun setupRatio(bottomSheetDialog: BottomSheetDialog) {
        val bottomSheet =
            bottomSheetDialog.findViewById<View>(com.google.android.material.R.id.design_bottom_sheet) as FrameLayout
        val behavior: BottomSheetBehavior<*> = BottomSheetBehavior.from(bottomSheet)
        val layoutParams = bottomSheet.layoutParams
        layoutParams.height = getWindowHeight()
        bottomSheet.layoutParams = layoutParams
        behavior.state = BottomSheetBehavior.STATE_EXPANDED
    }

    private fun getWindowHeight(): Int {
        return Resources.getSystem().displayMetrics?.heightPixels ?: 0
    }


#Text color change


     Common.setWordColor(
            channelName,
            getString(R.string.channel_delete_noti, channelName),
            "#FFEB6B44"
        )

      fun setWordColor(colorWord: String, resultText: String, color: String): SpannableStringBuilder {
      val ssb = SpannableStringBuilder(resultText)
      val start = resultText.indexOf(colorWord)
      if (start >= 0) {
          ssb.setSpan(
              ForegroundColorSpan(Color.parseColor(color)),
              start,
              start + colorWord.length,
              Spannable.SPAN_EXCLUSIVE_EXCLUSIVE
          )
      }
      return ssb
    }


 flutter file download with header 
 https://github.com/abdallah-odeh/flutter_file_downloader/issues/16




#flutter
provider -> riverpod 업글, 상태관리 pack, 
https://engineering.linecorp.com/ko/blog/flutter-architecture-getx-bloc-provider
https://seosh817.tistory.com/416


#android 6.0.1 shouldOverrideUrlLoading 못받는 오류
구버전 OS -> override fun shouldOverrideUrlLoading(view: WebView?, url: String?): Boolean {}
최신버전 OS -> override fun shouldOverrideUrlLoading(view: WebView?, request: WebResourceRequest?): Boolean {}


#android 14에서 MissingForegroundServiceType Error 발생하는경우
androidManifast.xml <service>에 android:foregroundServiceType 추가
https://developer.android.com/about/versions/14/behavior-changes-14?hl=ko#safer-intents

#android 14에서 '이 앱은 Android최신버전과 호환되지 않습니다. 업데이트를확인하거나 개발자에게 문의하세요'
32bit, 64bit 둘다 지원하는 단말에서 32bit so만 지원하도록 설정하는 경우 발생하는 팝업 둘다 지원하도록 수정 필요
https://github.com/flutter/flutter/issues/137895
https://cs.android.com/android/platform/superproject/main/+/main:frameworks/base/services/core/java/com/android/server/wm/AppWarnings.java;l=176?q=DeprecatedAbiDialog


#Bitmap too large to be uploaded into a texture 워닝 발생하는 경우
drawable 폴더에 이미지를 넣어놓고 설정 시 현재 해상도에 맞는 dip로 변환해서 처리하게됨, 해상도 상관없이 동일한 이미지 사이즈로 사용하고 싶을경우 drawable-nodip에 넣어야함


