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
