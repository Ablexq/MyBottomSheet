
参考：

[BottomSheetDialog的使用](https://blog.csdn.net/a254837127/article/details/54926040?locationNum=1&fps=1)

[BottomSheet、BottomSheetDialog使用详解](https://www.jianshu.com/p/0a7383e0ad0f)

behavior：
====

```
<android.support.v4.widget.NestedScrollView
    android:id="@+id/bottom_sheet"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    app:behavior_hideable="true"
    app:behavior_peekHeight="50dp"
    app:layout_behavior="@string/bottom_sheet_behavior">

</android.support.v4.widget.NestedScrollView>
```

app:behavior_peekHeight="50dp" 
peekHeight是当Bottom Sheets关闭的时候，底部我们能看到的高度,默认是0不可见。
behavior_peekHeight 对应代码 behavior.setPeekHeight(50);

app:behavior_hideable="true" 
hideable是当我们拖拽下拉的时候，bottom sheet是否能全部隐藏。
behavior_hideable 对应代码 behavior.setHideable(false);

layout_behavior指向bottom_sheet_behavior,代表这是一个bottom Sheets


监听

```
behavior.setBottomSheetCallback(new BottomSheetBehavior.BottomSheetCallback() {
    @Override
    public void onStateChanged(@NonNull View bottomSheet, int newState) {
        //这里是bottomSheet 状态的改变
        System.out.println("newState=======" + newState);
    }

    @Override
    public void onSlide(@NonNull View bottomSheet, float slideOffset) {
        //这里是拖拽中的回调，根据slideOffset可以做一些动画
        System.out.println("slideOffset=====" + slideOffset);
    }
});
```


newState的五种状态：
--
```
    /**
     * The bottom sheet is dragging.
     */
    public static final int STATE_DRAGGING = 1;//按住拖动

    /**
     * The bottom sheet is settling.
     */
    public static final int STATE_SETTLING = 2;
    //拖拽松开之后到达终点位置（collapsed or expanded）前的状态。

    /**
     * The bottom sheet is expanded.
     */
    public static final int STATE_EXPANDED = 3;//展开

    /**
     * The bottom sheet is collapsed.
     */
    public static final int STATE_COLLAPSED = 4; //折叠，部分可见

    /**
     * The bottom sheet is hidden.
     */
    public static final int STATE_HIDDEN = 5;   //不可见
```

slideOffset的值变化范围：
--
【-1到0到1】 ：表示【完全隐藏】到【完全展开】变化的百分比，



展开：
```
newState=======2
slideOffset=====-0.64666665
slideOffset=====0.0625
....
slideOffset=====1.0
newState=======3
```

折叠
```
newState=======2
slideOffset=====0.94895834
...
slideOffset=====0.0
newState=======4
```

手动隐藏
```
newState=======1
slideOffset=====-0.053333335
slideOffset=====-0.28666666
slideOffset=====-0.75333333
newState=======2
slideOffset=====-1.0
newState=======5
```

手动展开：
```
newState=======1
slideOffset=====0.010416667
slideOffset=====0.10520833
newState=======2
slideOffset=====0.63645834
...
slideOffset=====1.0
newState=======3
```




