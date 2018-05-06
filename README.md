# SimpleRecyclerViewAndroidExample
Simple RecyclerView example in android

 - Add library in build.gradle(Module.app)

	```
	dependencies {
    		implementation 'com.android.support:recyclerview-v7:27.1.1'
	}
	```

 - Add recyclerView in XML file

 	```
 	<android.support.v7.widget.RecyclerView
        android:id="@+id/rvDemo"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>
    ```

 - Create a XML file item.xml

 	```
 	<?xml version="1.0" encoding="utf-8"?>
	<LinearLayout
    	xmlns:android="http://schemas.android.com/apk/res/android"
    	android:layout_width="wrap_content"
    	android:layout_height="wrap_content"
    	android:orientation="horizontal"
    	android:padding="10dp">
    	<TextView
       		android:id="@+id/tvItem"
        	android:layout_width="wrap_content"
        	android:layout_height="wrap_content"
        	android:textSize="20sp"/>
	</LinearLayout>
	```

 - Create a class adapter

 	```
 	public class MyRecyclerViewAdapter extends RecyclerView.Adapter<MyRecyclerViewAdapter.ViewHolder> {

    	private List<String> arr;
    	private LayoutInflater mInflater;
    	private ItemClickListener mClickListener;

    	// constructor
   		MyRecyclerViewAdapter(Context context, List<String> data) {
        	this.mInflater = LayoutInflater.from(context);
        	this.arr = data;
    	}

    	@Override
    	public ViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {
        	View view = mInflater.inflate(R.layout.item, parent, false);
        	return new ViewHolder(view);
    	}

    	@Override
    	public void onBindViewHolder(ViewHolder holder, int position) {
        	String text = arr.get(position);
        	holder.myTextView.setText(text);
    	}

    	@Override
    	public int getItemCount() {
        	return arr.size();
    	}

    	public class ViewHolder extends RecyclerView.ViewHolder implements View.OnClickListener {
        	TextView myTextView;

        	ViewHolder(View itemView) {
            	super(itemView);
            	myTextView = itemView.findViewById(R.id.tvItem);
            	itemView.setOnClickListener(this);
        	}

        	@Override
        	public void onClick(View view) {
            	if (mClickListener != null) mClickListener.onItemClick(view, getAdapterPosition());
        	}
    	}

    	String getItem(int id) {
        	return arr.get(id);
    	}

    	void setClickListener(ItemClickListener itemClickListener) {
        	this.mClickListener = itemClickListener;
    	}

    	public interface ItemClickListener {
        	void onItemClick(View view, int position);
    	}
	}

	```

 - In MainActivity

 	```
 	public class MainActivity extends AppCompatActivity implements MyRecyclerViewAdapter.ItemClickListener {

    	MyRecyclerViewAdapter adapter;

    	@Override
    	protected void onCreate(Bundle savedInstanceState) {
        	super.onCreate(savedInstanceState);
        	setContentView(R.layout.activity_main);
        
        	ArrayList<String> arrayList = new ArrayList<>();
        	arrayList.add("One");
        	arrayList.add("Two");
        	arrayList.add("Three");
        	arrayList.add("Four");
        	arrayList.add("Five");
        
        	RecyclerView recyclerView = findViewById(R.id.rvDemo);
        	recyclerView.setLayoutManager(new LinearLayoutManager(this,LinearLayoutManager.VERTICAL,false));
        	adapter = new MyRecyclerViewAdapter(this, arrayList);
        	adapter.setClickListener(this);
        	recyclerView.setAdapter(adapter);
    	}

    	@Override
    	public void onItemClick(View view, int position) {
        	/// Do something
    	}
	}
	```

