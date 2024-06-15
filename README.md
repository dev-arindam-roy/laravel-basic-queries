# laravel Basic Queries

## Visit!
[https://laravelqueries.blogspot.com/](https://laravelqueries.blogspot.com/)

```php
[Ex # 1]
$data = test::all();


[Ex # 2]		
$data = test::all()->toArray();


[Ex # 3]		
$data = test::all()->toJson();


[Ex # 4]		
$data = DB::table('test')->get()->toArray();


[Ex # 5]		
$data = DB::table('test')->get()->toJson();


[Ex # 6]		
$data = test::find(1); // if not found array return null


[Ex # 7]		
$data = test::find([1,5,4]);


[Ex # 8]		
$data = test::find(1)->item;


[Ex # 9]		
$data = test::findOrFail(2); //if fail show 404


[Ex # 10]		
$data = test::where('price','>','5')->get();


[Ex # 11]		
$data = test::where('price','>','5')->take(1)->get(); // take as limit


[Ex # 12]		
$data = test::all()->count(); // return non array, only value


[Ex # 13]		
$data = test::where('price','>','15')->count();
		

[Ex # 14]	
$data = test::find(1);
$data->item = 'Item 100';
$data->save(); // that's mean update & return 1
		
		
[Ex # 15]		
$data = new test();
$data->item = 'Item 1000';
$data->price = '1000';
$data->qty = '1000';
$data->save(); // that's mean insert new record & return 1
		

[Ex # 16]		
$data = test::all()->max('price'); // return value not array


[Ex # 17]		
$data = DB::table('test')->get();


[Ex # 18]		
$data = DB::table('test')->count(); // return only value


[Ex # 19]		
$data = DB::table('test')->max('price'); // return only value


[Ex # 20]		
$data = DB::table('test')->min('price'); // return only value


[Ex # 21]		
$data = DB::table('test')->sum('price'); // return only value


[Ex # 22]		
$data = DB::table('test')->avg('price'); // return only value


[Ex # 23]		
$data = DB::table('test')->first();


[Ex # 24]		
$data = DB::table('test')->get()->first();


[Ex # 25]		
$data = DB::table('test')->get()->take(2);


[Ex # 26]		
$data = DB::table('test')->pluck('item'); // return all item name in array


[Ex # 27]		
$data = DB::table('test')->pluck('price','item'); // return key=>value array


[Ex # 28]		
$data = DB::table('test')->select('item','qty')->get();


[Ex # 29]		
$data = DB::table('test')->max('price');


[Ex # 30]		
$data = DB::table('test')->distinct()->get(); // return distinct rows


[Ex # 31]		
$data = DB::table('test')->select('item as Item_Name','qty as Item_QTY')->get(); // field naming


[Ex # 32]		
$data = DB::table('test')->whereBetween('qty',[8,20])->get();


[Ex # 33]		
$data = DB::table('test')->whereNotBetween('price',[50,200])->get();


[Ex # 34]		
$data = DB::table('test')->whereIn('id',[2,4,6])->get();


[Ex # 35]		
$data = DB::table('test')->whereNotIn('id',[2,4,6])->get();


[Ex # 36]		
$data = DB::table('test')->whereQty('10')->get(); // join table field with where clause


[Ex # 37]		
$data = DB::table('test')->whereIdAndQty('3','10')->get();


[Ex # 38]		
$data = DB::table('test')->whereIdOrQty('3','5')->get();


[Ex # 39]		
$data = DB::table('test')->skip(3)->take(4)->get(); // skip first 3 row and take 4 rows


[Ex # 40]		
$data = DB::table('test')->orderByRaw('RAND()')->take(2)->select('item')->get(); // get random items


[Ex # 41]		
$data = DB::table('test')->orderByRaw('RAND()')->take(2)->get(); // get random rows


[Ex # 42]		
$data = DB::table('test')->insert(['item'=>'Item 2000','price'=>'2000','qty'=>'20']); // return true


[Ex # 43]		
$data = DB::table('test')->insertGetId(['item'=>'Item 5000','price'=>'5000','qty'=>'50']); // return insert id


[Ex # 44]		
$data = DB::table('test')->increment('qty'); // increment 1 with all qty


[Ex # 45]		
$data = DB::table('test')->where('id','=',3)->increment('qty',10); // increment qty - 10 where id = 3


[Ex # 46]		
$data = DB::table('test')->where('id','=',5)->decrement('qty','4');


[Ex # 47]		
$data = DB::table('test')->delete(); // delete all , return how many row deleted


[Ex # 48]		
$data = DB::table('test')->where('id','=',3)->delete();


[Ex # 49]		
$data = DB::table('test')->truncate();
```
## LARAVEL MAX QUERY

```php
Using Model (way1)
$data = exampleModel::all()->max('salary');
dd($data);

Using Model (way2)
$data = exampleModel::get()->max('salary');
dd($data);

Using DB Query 
$data = DB::table('example_table')->max('age');
dd($data);

Example #1 
$data = DB::select(DB::raw('select * from example_table where id = (select max(`id`) from example_table)'));
dd($data);

Example #2 
$data = exampleModel::whereRaw('id = (select max(`id`) from example_table)')->get();
dd($data);

Example #3 
$data = DB::table('example_table')->find(DB::table('example_table')->max('id'));
dd($data);

Example #4 
$data = exampleModel::find(DB::table('example_table')->max('id'));
dd($data);
```
## LARAVEL MIN QUERY

```php
Using Model (way1)
$data = exampleModel::all()->min('salary');
dd($data);

Using Model (way2)
$data = exampleModel::get()->min('salary');
dd($data);

Using DB Query 
$data = DB::table('example_table')->min('age');
dd($data);

Example #1 
$data = DB::select(DB::raw('select * from example_table where id = (select min(`id`) from example_table)'));
dd($data);

Example #2 
$data = exampleModel::whereRaw('id = (select min(`id`) from example_table)')->get();
dd($data);

Example #3 
$data = DB::table('example_table')->find(DB::table('example_table')->min('id'));
dd($data);

Example #4 
$data = exampleModel::find(DB::table('example_table')->min('id'));
dd($data);

Example #5 
$data = exampleModel::where('id', '>', DB::table('example_table')->min('id'))
	->where('id', '<', DB::table('example_table')->max('id'))
  ->get();
dd($data);
```
