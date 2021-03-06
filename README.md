# dependent-dropdown-with-voyager
Dependent Dropdown Ajax with Voyager
 
# Install
Download zip https://github.com/d3turnes/dependent-dropdown-with-voyager/archive/master.zip and decompress the content in your project laravel

Edit the file routes/api.php and add the following code

```php

use Illuminate\Http\Request;

/*
|--------------------------------------------------------------------------
| API Routes
|--------------------------------------------------------------------------
|
| Here is where you can register API routes for your application. These
| routes are loaded by the RouteServiceProvider within a group which
| is assigned the "api" middleware group. Enjoy building your API!
|
*/

Route::middleware('auth:api')->get('/user', function (Request $request) {
   return $request->user();
});

Route::group(['prefix' => 'v1', 'as' => 'api.v1.', 'namespace' => 'Api\\V1\\'], function() {
   Route::post('/dependent-dropdown', ['uses' => 'DependentDropdownController@index', 'as' => 'dropdown']);
});

```

Edit the file app/Providers/AppServiceProvider.php and add the following code

```php

namespace App\Providers;

use Illuminate\Support\ServiceProvider;
use TCG\Voyager\Facades\Voyager;

use App\FormFields\SelectDependentDropdown;

class AppServiceProvider extends ServiceProvider
{
    /**
     * Bootstrap any application services.
     *
     * @return void
     */
    public function boot()
    {
        Voyager::addFormField(SelectDependentDropdown::class);
    }

    /**
     * Register any application services.
     *
     * @return void
     */
    public function register()
    {
        //
    }
}

```

# Example 1

Dependent Dropdown Ajax (Family/Subcategory)

families(id, name, slug)  
subcategories(id, name, slug, family_id)  
products(id, name, slug, price, dec, subcategory_id, created_at, updated_at)  

![list-products](https://raw.githubusercontent.com/d3turnes/storage/master/example1/list.png)
![add-products](https://raw.githubusercontent.com/d3turnes/storage/master/example1/add_new.png)
![edit-products](https://raw.githubusercontent.com/d3turnes/storage/master/example1/edit.png)


* move the content of /example1/models to /app
* move the content of /example1/database to /database

1. composer dumpautoload
2. php artisan migrate
3. php artisan db:seed --class=ProductsTableSeeder

![model-products](https://raw.githubusercontent.com/d3turnes/storage/master/example1/model.png)

* Definition
![bread-products](https://raw.githubusercontent.com/d3turnes/storage/master/example1/definition.png)

# Example 2

Dependent Dropdown Ajax (Country/State/City)

countries(id, name)  
states(id, name, country_id)  
cities(id, name, state_id)  
offices(id, name, slug, address, lat, lng, city_id)  

![add-offices](https://raw.githubusercontent.com/d3turnes/storage/master/example2/add_new.png)

* move the content of /example2/models to /app
* move the content of /example2/database to /database

1. composer dumpautoload
2. php artisan migrate
3. php artisan db:seed --class=CountriesTableSeeder
3. php artisan db:seed --class=StatesTableSeeder
3. php artisan db:seed --class=CitiesTableSeeder
3. php artisan db:seed --class=OfficesTableSeeder

![model-offices](https://raw.githubusercontent.com/d3turnes/storage/master/example2/model.png)

* Definition
![bread-defition-offices](https://raw.githubusercontent.com/d3turnes/storage/master/example2/bread_definition.png)
