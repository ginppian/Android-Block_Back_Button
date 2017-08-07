Android: Bloquear El Boton Back
==========

## Definición

<p align="justify">
    Al crear nuestro LogIn no queremos que el usuario pueda regresar a la pantalla de éste.
</p> 

## Desarrollo

* Activamos dos *banderas* y finalizamos la actividad con *finish()*

 ```
                        try{
    
                            Intent intent = new Intent(MainActivity.this, MapsActivity.class);
                            intent.putExtra("miCorreo", correo);
                            intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP);
                            intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
                            startActivity(intent);
                            finish();
    
                        }catch(Exception e){
                            Log.d("what",e.getMessage());
                        }
 ```
 
 * En el siguiente activity agregamos los métodos: *onBackPressed* y *onKeyDown* para bloquear el boton.
 
 ```
 public class MapsActivity extends FragmentActivity implements OnMapReadyCallback {
 
     // Share Info
     private Bundle bundle;
 
     // Google Maps
     private GoogleMap mMap;
     private Marker marcador;
     double lat = 0.0;
     double lng = 0.0;
 
     @Override
     protected void onCreate(Bundle savedInstanceState) {
         super.onCreate(savedInstanceState);
         setContentView(R.layout.activity_maps);
 
         // Obtain the SupportMapFragment and get notified when the map is ready to be used.
         SupportMapFragment mapFragment = (SupportMapFragment) getSupportFragmentManager()
                 .findFragmentById(R.id.map);
         mapFragment.getMapAsync(this);
 
         loadView();
     }
 
     private void loadView(){
 
         // Get Var MainActivity
         bundle = getIntent().getExtras();
         String correo = bundle.getString("miCorreo").toString();
 
         // Set title ActionBar
         //getActionBar().setTitle(correo);
         //getSupportActionBar().setTitle(correo);
     }
 
     // Block Back Button
     @Override
     public void onBackPressed() {
         moveTaskToBack(false);
     }
 
     // Block Back
     @Override
     public boolean onKeyDown(int keyCode, KeyEvent event) {
         if(keyCode== KeyEvent.KEYCODE_BACK) {
             return false;
         }
         return super.onKeyDown(keyCode, event);
     }
 ```
 
 ## Fuente
 
 * <a href="https://stackoverflow.com/questions/8631095/android-preventing-going-back-to-the-previous-activity">Android: Preventing going back to the previous activity</a>
 * <a href="https://sourcey.com/beautiful-android-login-and-signup-screens-with-material-design/">Beautiful Android Login and Signup Screens</a>