# Navigation Design using Kotlin
# Android Studio

At the End Application Looks Like:

![Screenshot1](https://user-images.githubusercontent.com/78692972/171831011-81b61003-fcf3-4ca9-ad5d-b93f66c34a36.jpg)

Steps to Create Navigation Drawer 
1. Add Two Dependency In **Gradle Scripts | build.gradle | module: Project_name.app**
          
          implementation 'androidx.navigation:navigation-fragment-ktx:2.4.2'
          implementation 'androidx.navigation:navigation-ui-ktx:2.4.2'

2. Create the New .xml file in **Layout |** Named as drawer_header

          <?xml version="1.0" encoding="utf-8"?>
          <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
              android:layout_width="match_parent"
              android:layout_height="250dp"
              android:orientation="vertical"
              android:background="#5BBBE8">

            <ImageView
              android:layout_width="180dp"
              android:layout_height="180dp"
              android:src="@drawable/educationlogo" />

            <TextView
              android:layout_width="wrap_content"
              android:layout_height="wrap_content"
              android:text="@string/navigation_design_a"
              android:textStyle="bold"
              android:padding="10dp"
              android:textSize="25sp"
              android:layout_marginTop="20dp"/>
        </LinearLayout>

Output: 

![image](https://user-images.githubusercontent.com/78692972/171831989-e878eb75-8987-4106-9a42-c5d45b32cd52.png)


3. Add Image Asset in **Drawable** 

![image](https://user-images.githubusercontent.com/78692972/171832492-612af755-5deb-4478-ad16-f91d5d728269.png)

  Image asset
  Simply Go to **Drawable | new | Image Asset**
  ![Screenshot (259)](https://user-images.githubusercontent.com/78692972/171832951-375b8933-94c3-4723-be19-aa7b5e818d5b.png)
  
  ![image](https://user-images.githubusercontent.com/78692972/171832719-bfc786ea-0e8c-4366-8eff-4f1649a933bf.png)

4. Create **menu** directory in res folder
res | new | directory 

5. now make new .xml layout in menu directory names as *menu_drawer.xml*
    
       <?xml version="1.0" encoding="utf-8"?>
       <menu xmlns:android="http://schemas.android.com/apk/res/android">
          <group android:checkableBehavior="single">

            <item
                android:id="@+id/dashboard"
                android:icon="@drawable/ic_action_dash"
                android:title="@string/dashboard" />

            <item
                android:id="@+id/favourites"
                android:icon="@drawable/ic_action_fav"
                android:title="@string/favourites" />

            <item
                android:id="@+id/profile"
                android:icon="@drawable/ic_action_pro"
                android:title="@string/profile" />

            <item
                android:id="@+id/about"
                android:icon="@drawable/ic_action_info"
                android:title="@string/about" />

            <item
                android:id="@+id/setting"
                android:icon="@drawable/ic_action_sett"
                android:title="@string/settings" />
          </group>
        </menu>

Output:
![image](https://user-images.githubusercontent.com/78692972/171834462-8fa56cd1-3a3f-4e5e-a1c1-2699c6fc5a27.png)

6. Then Create the blank fragments
  *com.surajpatil.navigationdrawer1 | new | fragments | blank Fragments*
  
7. Paste the Code in MainActivity.kt file


       <?xml version="1.0" encoding="utf-8"?>
       <androidx.drawerlayout.widget.DrawerLayout xmlns:android="http://schemas.android.com/apk/res/android"
       xmlns:app="http://schemas.android.com/apk/res-auto"
       xmlns:tools="http://schemas.android.com/tools"
       android:layout_width="match_parent"
       android:layout_height="match_parent"
       android:id="@+id/drawerLayout"
       tools:context=".MainActivity">

       <androidx.coordinatorlayout.widget.CoordinatorLayout
        android:id="@+id/coordinatorLayout"
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <com.google.android.material.appbar.AppBarLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:theme="@style/ThemeOverlay.AppCompat.Dark"
            android:elevation="0dp">

            <androidx.appcompat.widget.Toolbar
                android:id="@+id/toolbar"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:background="#5BBBE8"
                android:minHeight="?attr/actionBarSize"
                android:theme="@style/ThemeOverlay.AppCompat.Dark"
                app:layout_scrollFlags="scroll|enterAlways"/>

        </com.google.android.material.appbar.AppBarLayout>

        <FrameLayout
            android:id="@+id/frame"
            android:layout_width="fill_parent"
            android:layout_height="fill_parent"
            app:layout_behavior="@string/appbar_scrolling_view_behavior"/>

       </androidx.coordinatorlayout.widget.CoordinatorLayout>


       <com.google.android.material.navigation.NavigationView
        android:id="@+id/navigationView"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:headerLayout="@layout/drawer_header"
        app:menu="@menu/menu_drawer"
        android:layout_gravity="start"/>

       </androidx.drawerlayout.widget.DrawerLayout>

8. Paste the Code in MainActivity.kt file

       package com.surajpatil.navigationdrawer1
       
       import androidx.appcompat.app.AppCompatActivity
       import android.os.Bundle
       import android.view.MenuItem
       import android.widget.FrameLayout
       import android.widget.Toast
       import androidx.appcompat.app.ActionBarDrawerToggle
       import androidx.appcompat.widget.Toolbar
       import androidx.coordinatorlayout.widget.CoordinatorLayout
       import androidx.core.view.GravityCompat
       import androidx.drawerlayout.widget.DrawerLayout
       import com.google.android.material.navigation.NavigationView
       import com.surajpatil.navigationdrawer1.fragments.*

       class MainActivity : AppCompatActivity() {


       lateinit var drawerLayout: DrawerLayout
       lateinit var coordinatorLayout: CoordinatorLayout
       lateinit var toolbar: Toolbar
       lateinit var frameLayout: FrameLayout
       lateinit var navigationView: NavigationView

       var previousMenuItem : MenuItem?= null

        override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        drawerLayout = findViewById(R.id.drawerLayout)
        coordinatorLayout = findViewById(R.id.coordinatorLayout)
        toolbar = findViewById(R.id.toolbar)
        frameLayout = findViewById(R.id.frame)
        navigationView = findViewById(R.id.navigationView)

        // calling function setUpToolbar
        setUpToolbar()

        // by default open dashboard fragment
        openDashboard()

        val actionBarDrawerToggle = ActionBarDrawerToggle(
            this@MainActivity ,
            drawerLayout ,
            R.string.open_drawer ,
            R.string.close_drawer
        )

        drawerLayout.addDrawerListener(actionBarDrawerToggle)

        // back arrow and hamburger icon vice-virca
        actionBarDrawerToggle.syncState()

        navigationView.setNavigationItemSelectedListener {

            if(previousMenuItem != null)
            {
                previousMenuItem?.isChecked = false
            }

            it.isCheckable = true
            it.isChecked = true
            previousMenuItem = it

            when (it.itemId) {
                R.id.dashboard -> {
                    Toast.makeText(this@MainActivity , "Clicked On Dashboard" , Toast.LENGTH_SHORT)
                        .show()

                    supportFragmentManager.beginTransaction().replace(R.id.frame , DashboardFragment()).commit()

                    supportActionBar?.title = "Dashboard"
                    drawerLayout.closeDrawers()
                }
                R.id.favourites -> {
                    Toast.makeText(this@MainActivity , "Clicked On Favourites" , Toast.LENGTH_SHORT)
                        .show()

                    supportFragmentManager.beginTransaction().replace(R.id.frame , FavouritesFragment()).commit()

                    supportActionBar?.title = "Favourites"
                    drawerLayout.closeDrawers()
                }
                R.id.profile -> {
                    Toast.makeText(this@MainActivity , "Clicked On Profile" , Toast.LENGTH_SHORT)
                        .show()

                    supportFragmentManager.beginTransaction().replace(R.id.frame , ProfileFragment()).commit()

                    supportActionBar?.title = "Profile"
                    drawerLayout.closeDrawers()
                }
                R.id.setting -> {
                    Toast.makeText(this@MainActivity , "Clicked On Settings" , Toast.LENGTH_SHORT)
                        .show()

                    supportFragmentManager.beginTransaction().replace(R.id.frame , SettingsFragment()).commit()

                    supportActionBar?.title = "Settings"
                    drawerLayout.closeDrawers()
                }
                R.id.about -> {
                    Toast.makeText(this@MainActivity , "Clicked On About App" , Toast.LENGTH_SHORT)
                        .show()

                    supportFragmentManager.beginTransaction().replace(R.id.frame , AboutFragment()).commit()

                    supportActionBar?.title = " About App"
                    drawerLayout.closeDrawers()
                }
            }

            return@setNavigationItemSelectedListener true
        }
       }

       fun setUpToolbar() {
        setSupportActionBar(toolbar)
        supportActionBar?.title = "Toolbar Title"
        supportActionBar?.setHomeButtonEnabled(true)
        supportActionBar?.setDisplayHomeAsUpEnabled(true)
       }


       override fun onOptionsItemSelected(item: MenuItem): Boolean {
        val id = item.itemId
        if (id == android.R.id.home) {
            drawerLayout.openDrawer(GravityCompat.START)
        }
        return super.onOptionsItemSelected(item)
       }

       fun openDashboard()
       {
        val fragment = DashboardFragment()
        val transcation = supportFragmentManager.beginTransaction()
        transcation.replace(R.id.frame, fragment)
        transcation.commit()
        supportActionBar?.title = "Dashboard"
        navigationView.setCheckedItem(R.id.dashboard)
       }

       override fun onBackPressed() {
        val frag = supportFragmentManager.findFragmentById(R.id.frame)

        when(frag)
        {
            !is DashboardFragment -> openDashboard()

            else -> super.onBackPressed()
         }
        }
       }





