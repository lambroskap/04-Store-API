<h1>
<span style = "color: cyan">
Store API Project
</span>
</h1>

The main idea of this project is to allow users to perform **GET** requests both static but also dynamically in order to get products that are defined in a **MongoDB** database. The products that are being displayed follow some critecia.

## Installation 

In order to run this project all you need to do is to install the packages that are defined in **package.json** from your terminal.You can simply install them by running :

```
npm install 
```

Finally in order to make the server running use the command:

```
npm start
```

> Our server is now listening on **localhost:3000**

<h2>
<span style = "color: cyan">
Static GET Request
</span>
</h2>

In order to perform this request we navigate to:

> ***localhost:3000/api/v1/products/static***

The filters that are used to find products from the database have already being defined. All products that are being displayed matches the following criteria:

> - price > 30 
> - products are sorted based on price (lowest-highest)
> - and we display only the name-price properties for each one

Feel free to change the criteria by changing the code that is stored in file **products.js** in **controllers** directory.

### Examples

```
const getAllProductsStatic = async (req,res)=>{
    const products = await Product.find({price: {$gt: 40}})
    .sort("-price")
    .select("name rating");
    res.status(200).json({products, nbHits: products.length});
}
```

Now we have changed the find method to come up with products with price > 40, then we sort those products (from highest - lowest) and finally we display only the name and rating properties. 

<h2>
<span style = "color: cyan">
Dynamically GET Request
</h2>

To perform this request we navigate to:

> ***localhost:3000/api/v1/products/***

After the "/" we can define our own queries based on:

> - product properties
>    - featured
>    - company
>    - name
> - sort 
> - fields to be displayed
> - numericFilters
> - pagination

### Examples

> ***localhost:3000/api/v1/products?featured=false&
>company=ikea***

> ***localhost:3000/api/v1/products?featured=false&
>company=liddy&sort=name***

> ***localhost:3000/api/v1/products?company=ikea&sort=-name&
> fields=name,price***

> ***localhost:3000/api/v1/products?company=caressa&sort=name&
> numericFilters=price>40,rating>=4***

> ***localhost:3000/api/v1/products?company=caressa&sort=name&
> page=2***