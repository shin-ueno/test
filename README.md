# Main_activity
package com.example.timerthreadtest;

import java.util.Timer;
import java.util.TimerTask;

import android.app.Activity;
import android.graphics.Color;
import android.os.Bundle;
import android.os.Handler;
import android.view.View;
import android.view.Window;
import android.widget.Button;
import android.widget.LinearLayout;
import android.widget.TextView;

import com.example.timertest.R;

public class MainActivity extends Activity {

    private int count = 0;
    private Button startbtn;
    private Button stopbtn;
    private TextView tv;
    private Handler handler = new Handler();
    private Timer mytimer = new Timer();

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        requestWindowFeature(Window.FEATURE_NO_TITLE);

        LinearLayout ll = new LinearLayout(this);
        ll.setBackgroundColor(Color.WHITE);
        ll.setOrientation(LinearLayout.VERTICAL);
        setContentView(ll);

        startbtn = (Button)findViewById(R.id.startbtn);
        stopbtn = (Button)findViewById(R.id.stopbtn);

        startbtn.setOnClickListener(new View.OnClickListener() {

			@Override
			public void onClick(View v) {
				// タイマースタート
		        mytimer.schedule(new MyTimer(), 0, 1000);
			}
		});

        stopbtn.setOnClickListener(new View.OnClickListener() {

			@Override
			public void onClick(View v) {
				// タイマーストップ
				mytimer.cancel();
			}
		});

        tv = new TextView(this);
        tv.setBackgroundColor(Color.rgb(224, 224, 224));
        tv.setTextColor(Color.GREEN);
        tv.setText("ボタンを押して");
        ll.addView(tv);
    }

    public void onResume() {
        super.onResume();
    }

    public void onPause() {
        super.onPause();
        mytimer.cancel();
    }

    private class MyThread extends Thread {
        public void run() {
            handler.post(new Runnable(){
                public void run() {
                    tv.setText("count=" + count++);
                }
            });
        }
    }

    private class MyTimer extends TimerTask {
        public void run() {
            MyThread mythread = new MyThread();
            mythread.start();
        }
    }
}

# activity_main
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context="com.example.timertest.MainActivity" >

    <Button
        android:id="@+id/startbtn"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginLeft="14dp"
        android:text="start" />

    <Button
        android:id="@+id/stopbtn"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignBaseline="@+id/startbtn"
        android:layout_alignBottom="@+id/startbtn"
        android:layout_alignParentRight="true"
        android:layout_marginRight="57dp"
        android:text="Button" />

</RelativeLayout>
