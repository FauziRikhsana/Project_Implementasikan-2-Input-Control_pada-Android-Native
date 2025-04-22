# Project_Implementasikan-2-Input-Control_pada-Android-Native
<ul>
  <li>Mata Kuliah:Pemograman Mobile 1 </li>
  <li>Dosen Pengampu: Nova Agustina, ST., M.Kom.</li>
</ul>

## Profil
<ul>
  <li>Nama: Fauzi Rikhshana</li>
  <li>NIM: 23552011030</li>
  <li>Kelas: TIF CNS C</li>
</ul>

## source code XML Layout (activity_main.xml)
<p>
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/rootLayout"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="24dp">

    -- Date Picker Button --
    <Button
        android:id="@+id/btnPickDate"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Pick Date" />

    -- Time Picker Button --
    <Button
        android:id="@+id/btnPickTime"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Pick Time"
        android:layout_marginTop="8dp"/>

    -- Display Date and Time --
    <TextView
        android:id="@+id/tvDateTime"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Selected Date & Time"
        android:layout_marginTop="12dp"
        android:textSize="16sp" />

    -- Input Phone Number --
    <EditText
        android:id="@+id/etPhone"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter Phone Number"
        android:inputType="phone"
        android:layout_marginTop="24dp"/>

    -- Submit Phone Number --
    <Button
        android:id="@+id/btnSubmit"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Submit Phone"
        android:layout_marginTop="8dp"/>
</LinearLayout>

## Kotlin Activity (MainActivity.kt)
class MainActivity : AppCompatActivity() {

    private lateinit var tvDateTime: TextView
    private lateinit var btnPickDate: Button
    private lateinit var btnPickTime: Button
    private lateinit var etPhone: EditText
    private lateinit var btnSubmit: Button

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        tvDateTime = findViewById(R.id.tvDateTime)
        btnPickDate = findViewById(R.id.btnPickDate)
        btnPickTime = findViewById(R.id.btnPickTime)
        etPhone = findViewById(R.id.etPhone)
        btnSubmit = findViewById(R.id.btnSubmit)

        // Date Picker
        btnPickDate.setOnClickListener {
            val calendar = Calendar.getInstance()
            val datePicker = DatePickerDialog(this,
                { _, year, month, day ->
                    tvDateTime.text = "Date: $day/${month + 1}/$year"
                },
                calendar.get(Calendar.YEAR),
                calendar.get(Calendar.MONTH),
                calendar.get(Calendar.DAY_OF_MONTH))
            datePicker.show()
        }

        // Time Picker
        btnPickTime.setOnClickListener {
            val calendar = Calendar.getInstance()
            val timePicker = TimePickerDialog(this,
                { _, hour, minute ->
                    val current = tvDateTime.text.toString()
                    tvDateTime.text = "$current\nTime: $hour:$minute"
                },
                calendar.get(Calendar.HOUR_OF_DAY),
                calendar.get(Calendar.MINUTE),
                true)
            timePicker.show()
        }

        // Phone Number Submission
        btnSubmit.setOnClickListener {
            val phone = etPhone.text.toString().trim()
            if (phone.isEmpty()) {
                Toast.makeText(this, "Phone number cannot be empty", Toast.LENGTH_SHORT).show()
            } else {
                AlertDialog.Builder(this)
                    .setTitle("Confirm Phone Number")
                    .setMessage("Is this your number?\n$phone")
                    .setPositiveButton("Yes") { _, _ ->
                        Toast.makeText(this, "Phone number saved: $phone", Toast.LENGTH_LONG).show()
                    }
                    .setNegativeButton("No", null)
                    .show()
            }
        }
    }
}

</p>
