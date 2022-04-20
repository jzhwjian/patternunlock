# -PatternLockView开源库使用
屏幕图案解锁控件
支持手势滑动解锁绘制

1.Gradle
compile 'com.andrognito.patternlockview:patternlockview:1.0.0'
// Optional, for RxJava2 adapter
compile 'com.andrognito.patternlockview:patternlockview-reactive:1.0.0'

2.layout
<com.andrognito.patternlockview.PatternLockView
    android:id="@+id/patternlockview"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"

    app:dotCount="3"
    app:dotNormalSize="12dp"
    app:dotSelectedSize="24dp"
    app:pathWidth="4dp"
    app:aspectRatio="square"
    app:aspectRatioEnabled="true"
    app:normalStateColor="@color/white"
    app:correctStateColor="@color/design_default_color_primary"
    app:wrongStateColor="@color/teal_200"
    app:dotAnimationDuration="200"
    app:pathEndAnimationDuration="100"


    app:layout_constraintBottom_toBottomOf="parent"
    app:layout_constraintLeft_toLeftOf="parent"
    app:layout_constraintRight_toRightOf="parent"
    app:layout_constraintTop_toTopOf="parent" />
    
    3.
      PatternLockView patternLockView;
      String TAG = "Jeffmoss";
      String savePass="0124678";//现实是使用图案保存数据
    
      patternLockView = (PatternLockView)findViewById(R.id.patternlockview);
      patternLockView.setViewMode(PatternLockView.PatternViewMode.CORRECT);
      // patternLockView.setInStealthMode(true); //异常
      patternLockView.setTactileFeedbackEnabled(true);
      //patternLockView.setInputEnabled(false);//异常
      
       patternLockView.addPatternLockListener(new PatternLockViewListener() {
            @Override
            public void onStarted() {
                Log.i(TAG,"start");
            }

            @Override
            public void onProgress(List<PatternLockView.Dot> progressPattern) {
                Log.i(TAG,"onProgress:"+ PatternLockUtils.patternToString(patternLockView,progressPattern));
            }

            @Override
            public void onComplete(List<PatternLockView.Dot> pattern) {
                Log.i(TAG,"onComplete:"+PatternLockUtils.patternToString(patternLockView,pattern));
                String passwd = PatternLockUtils.patternToString(patternLockView,pattern);
                if(passwd.length()>=4 && savePass.equals(passwd)){
                    Toast.makeText(MainActivity.this,"密码验证成功",Toast.LENGTH_LONG).show();

                }else{
                    Toast.makeText(MainActivity.this,"密码验证失败",Toast.LENGTH_LONG).show();
                }
                patternLockView.clearPattern();
              //  patternLockView.clearPattern();

            }

            @Override
            public void onCleared() {
                Log.i(TAG,"onCleared");
            }
        });

    }
