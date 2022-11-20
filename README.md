## # Notepad #

## 期中实验

一、NoteList显示时间戳

二、笔记查询

三、笔记编辑

四、更改背景

五、ui美化



### 一、NoteList显示时间戳

### 效果图：

![](images/time.png)

### 关键代码：



	package com.example.android.notepad.util;
	
	import java.text.SimpleDateFormat;
	import java.util.Date;
	
	public class DateUtil {
	    public static String StringToDate(String str_data)
	    {
	        String beginDate=str_data;
	        SimpleDateFormat sdf=new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
	        String sd = sdf.format(new Date(Long.parseLong(beginDate)));
	        return  sd;
	    }
	}



### 二、笔记查询（根据标题查询）

### 效果图：

![](images/search.png)

### 关键代码：

'''

	package com.example.android.notepad.bean;
	
	import android.database.Cursor;
	
	public class NoteBean {
	    private String Title;//笔记的标题
	    private String createTime;//笔记的创建时间
	    private String Cursor_id;//所属的游标的position
	
	    public NoteBean(String title, String createTime) {
	        Title = title;
	        this.createTime = createTime;
	    }
	
	    public NoteBean(String title, String createTime, String cursor_id) {
	        Title = title;
	        this.createTime = createTime;
	        Cursor_id = cursor_id;
	    }
	
	    public NoteBean(String title, String createTime, String cursor_id, Cursor cursor) {
	        Title = title;
	        this.createTime = createTime;
	        Cursor_id = cursor_id;
	    }
	
	    public String getTitle() {
	        return Title;
	    }
	
	    public void setTitle(String title) {
	        Title = title;
	    }
	
	    public String getCreateTime() {
	        return createTime;
	    }
	
	    public void setCreateTime(String createTime) {
	        this.createTime = createTime;
	    }
	
	    public String getCursor_id() {
	        return Cursor_id;
	    }
	
	    public void setCursor_id(String cursor_id) {
	        Cursor_id = cursor_id;
	    }
	}



### 三、笔记编辑

### 效果图：

![](images/bianji.png)
![](images/bianji2.png)

### 关键代码：

	

	package com.example.android.notepad.util;


​	

	import android.content.Context;
	import android.content.SharedPreferences;
	import com.example.android.notepad.application.MyApplication;


​	
​	

	public class SharedPreferenceUtil {
	
	    private static String FILENAME = "Config";


​	

	    public static boolean CommitDate(String key, String date) {
	        SharedPreferences sp = MyApplication.getContext().getSharedPreferences(FILENAME, Context.MODE_PRIVATE);
	        SharedPreferences.Editor editor = sp.edit();
	        editor.putString(key, date);
	        return editor.commit();
	    }


​	

	    public static void ApplyDate(String key, String date) {
	        SharedPreferences sp = MyApplication.getContext().getSharedPreferences(FILENAME, Context.MODE_PRIVATE);
	        SharedPreferences.Editor editor = sp.edit();
	        editor.putString(key, date);
	        editor.apply();
	    }
	
	    /*
	    *获取数据
	     */
	    public static String getDate(String key) {
	        SharedPreferences sp = MyApplication.getContext().getSharedPreferences(FILENAME, Context.MODE_PRIVATE);
	        String str = sp.getString(key, "");
	        if (!str.isEmpty()) {
	            return str;
	        } else {
	            return null;
	        }
	    }
	

### 

#### 四、更改背景

### 效果图：

![](images/beijing1.png)
![](images/beijing2.png)
![](images/beijing3.png)

### 关键代码：



	package com.example.android.notepad.application;
	
	import android.app.Application;
	import android.content.Context;
	import android.util.Log;
	import com.example.android.notepad.util.SharedPreferenceUtil;
	
	public class MyApplication extends Application {
	
	    private static Context context;
	    private static String background="#ffffff";//背景颜色的十六进制值,默认为白色
	
	    @Override
	    public void onCreate() {
	        super.onCreate();
	        context=getApplicationContext();
	        readBackground();
	    }
	
	    public static Context getContext() {
	        return context;
	    }
	
	    public static void setContext(Context context) {
	        MyApplication.context = context;
	    }
	
	    public static String getBackground() {
	        return background;
	    }
	
	    public static void setBackground(String background) {
	        MyApplication.background = background;
	    }
	
	    /*
	        读取配置文件中的背景颜色
	         */
	    public static void readBackground(){
	        if(SharedPreferenceUtil.getDate("background")==null||SharedPreferenceUtil.getDate("background").equals("")){
	
	        }
	        else{
	            background= SharedPreferenceUtil.getDate("background");
	        }
	    }
	
	    /*读取配置文件中的背景颜色*/
	    public static void saveBackground(){
	        SharedPreferenceUtil.CommitDate("background",background);
	    }
	}



#### 五、ui美化

### 效果图：

![](images/UI.png)

### 关键代码：

'''

	<LinearLayout
        android:layout_width="match_parent"
        android:layout_height="1dp"
        android:background="#00000000"
        android:layout_marginTop="10dp"
        >

    </LinearLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:background="@drawable/yuan"
        android:orientation="horizontal"
        android:padding="5dp">

        <ImageView
            android:layout_width="55dp"
            android:layout_height="46dp"
            android:layout_marginTop="5dp"
            android:background="@drawable/wenjian" />

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:orientation="vertical">

            <TextView
                android:id="@+id/tv_title"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_marginLeft="10dp"
                android:layout_marginTop="5dp"
                android:text="Title"
                android:textColor="#3F51B5"
                android:textSize="20sp" />

            <TextView
                android:id="@+id/tv_data"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_marginLeft="80dp"
                android:layout_marginTop="2dp"
                android:text="2017/4/25 16:25:30"
                android:textColor="#000000" />
        </LinearLayout>

        <LinearLayout
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginTop="10dp"
            android:orientation="horizontal">

            <ImageView
                android:id="@+id/iv_editNote"
                android:layout_width="40dp"
                android:layout_height="40dp"
                android:layout_marginRight="10dp"
                android:background="@drawable/ic_menu_edit" />

            <ImageView
                android:id="@+id/iv_deleteNote"
                android:layout_width="0dp"
                android:layout_height="0dp"
                android:background="@drawable/ic_menu_delete" />
        </LinearLayout>

    </LinearLayout>


'''
