# Laragenerator

## Laravel 5.4 generator

Building a laravel project comes from an idea. So why not to build the main idea behavior and leave the rest to Laragenerator in order to bootstrap your project. 
This package helps you to focus more about your project idea. <b>DRY</b>.

The current features help you to :
````
- Create Namespaces.
- Create Controllers.
- Create Form Requests.
- Create Models.
- Create Models Relationships.
- Create Migrations.
- Create Routes Files.
- Create Views files.
````

If you have any suggestions please let me know : https://github.com/AbdelilahLbardi/Laragenerator/pulls.

## Installation

First, pull in the package through Composer.

```
"require": {
    "laracasts/generators": "master@dev",
    "abdelilahlbardi/laragenerator": "^1.5"
}
```

And then run :

```
composer update
```

After that, include the service provider within `config/app.php`.

```
'providers' => [
    AbdelilahLbardi\LaraGenerator\Providers\LaraGeneratorServiceProvider::class,
];
```

## Usage

The package extends Laravel Artisan and add `generate:resource` command :

Here's a quick example of how to bootstrap your laravel idea:

```bash
php artisan generate:resource Backend/Article "titles:string, content:text"
```

<table>
	<tr>
		<td>Name</td>
		<td>Type</td>
		<td>Exemple</td>
		<td>Usage</td>
	</tr>
	<tr>
		<td>Model</td>
		<td>Argument</td>
		<td>Backend/Article</td>
		<td><b>Required</b></td>
	</tr>
	<tr>
		<td>Schema</td>
		<td>Argument</td>
		<td>--schema="title:string, content:text, slug:string:unique"</td>
		<td>optional</td>
	</tr>
	<tr>
		<td>Relationships</td>
		<td>Option</td>
		<td>--relations="hasmany:tags, belongsto:user"</td>
		<td>optional</td>
	</tr>
	<tr>
		<td>Without controller</td>
		<td>Option</td>
		<td>--without-controller</td>
		<td>optional</td>
	</tr>
	<tr>
		<td>Without model</td>
		<td>Option</td>
		<td>--without-model</td>
		<td>optional</td>
	</tr>
	<tr>
		<td>Without request</td>
		<td>Option</td>
		<td>--without-request</td>
		<td>optional</td>
	</tr>
	<tr>
		<td>Without views</td>
		<td>Option</td>
		<td>--without-views</td>
		<td>optional</td>
	</tr>
	<tr>
		<td>Without routes</td>
		<td>Option</td>
		<td>--without-routes</td>
		<td>optional</td>
	</tr>
	<tr>
		<td>Without migration</td>
		<td>Option</td>
		<td>--without-migration</td>
		<td>optional</td>
	</tr>
	<tr>
		<td>Use flash</td>
		<td>Option</td>
		<td>--with-flash</td>
		<td>optional</td>
	</tr>
	<tr>
		<td>Rollback</td>
		<td>Option</td>
		<td>--rollback</td>
		<td>optional</td>
	</tr>
</table>

## Examples

- [Bootstrapping with all the resources](#bootstrapping-with-all-the-resources)
- [Bootstrapping without the model](#bootstrapping-without-the-model)
- [Bootstrapping with empty migration](#bootstrapping-with-empty-migration)
- [Delete the created files](#rollback)


### Bootstrapping with all the resources

  ```bash
php artisan generate:resource Article "title:string, content:text, slug:string:unique, user_id:integer:foreign"
```
You will notice additional files and folders appearing in your project :

 - `Controllers/ArticlesController.php` : Here your generated controller inside the namespace that you specified.
 - `app/Models/Article` : New Models folder the your Models.
 - `resources/views/articles/index.blade.php` : index view which is empty.
 - `resources/views/articles/create.blade.php` : empty create view.
 - `resources/views/articles/edit.blade.php` : empty edit view.
 - `routes/web/articles.php` : Ready routes generated.
 - `database/migrations/yyyy-mm-dd-create_articles_table.php` : Here your migration.


### Bootstrapping without the model

  ```bash
php artisan generate:resource Backed/Item "title:string, price:float, slug:string:unique, category_id:integer:foreign" --without-model
```
This will generate the same files as the recent command but will no include :

 - `Controllers/Backend/ItemsController.php` : Here your generated controller inside the namespace that your specified.
 - `resources/views/backend/items/index.blade.php` : index view which is empty.
 - `resources/views/backend/items/create.blade.php` : empty create view.
 - `resources/views/backend/items/edit.blade.php` : empty edit view.
 - `routes/web/backend/items.php` : Ready routes generated.
 - `database/migrations/yyyy-mm-dd-create_items_table.php` : Here your migration.
 
 ### Bootstrapping with empty migration

Since `--schema` is an optional option, if you don't specify the `--schema` option, Laragenerator generates an empty model with a simple id and timestamps.

To do so, here's a simple command.
  ```bash
php artisan generate:resource Backed/Item
```

The migration file will look like:

  ````php
  
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Database\Migrations\Migration;

class CreateItemsTable extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::create('items', function (Blueprint $table) {
            $table->increments('id');
            
            $table->timestamps();
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::drop('items');
    }
}
  
  ````

### Rollback

  ```bash
php artisan generate:resource Frontend/User --rollback
```
<p>With the Laragenerator `--rollback` option, you don't need to delete the generated folders manually. It does all the job for you.</p>
<p>Notice that if you have more controllers this options doesn't delete all the controllers in the namespace.</p>

## Templates publishing

You may want to customize the templates like the following artisan command:

```bash
php artisan vendor:publish --tag=templates
```

This will add a new folder to your app called `Tempaltes` where you will find the following files:

 - `Templates/Controller/Controller.txt` : Controllers Template.
 - `Templates/Model/Model.txt` : Models Template.
 - `Templates/View/index.txt` : Index View Template.
 - `Templates/View/headerCell.txt` : HTML table element header row Template.
 - `Templates/View/contentCell.txt` : HTML table element content rows Template.
 - `Templates/View/create.txt` : Create View Template.
 - `Templates/View/createInput.txt` : Create form inputs View Template.
 - `Templates/View/edit.txt` : Edit View Template.
 - `Templates/View/editInput.txt` : Edit form inputs View Template.
 - `Templates/routes.txt`: Routes File Tempalte.

## Schema

<p>Since Laragenerator uses https://github.com/laracasts/Laravel-5-Generators-Extended to generate migration and schema</p> 
<p>you can find the related documentation here: https://github.com/laracasts/Laravel-5-Generators-Extended. </p>
