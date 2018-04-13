<div dir='rtl'>
مراحل ثبت مقصد بسته
  </div>
  
  
  ```
   POST  /api/v{version}/post-pack 
  ```
  
<div dir='rtl'>
آدرس بالا دارای یک پارمتر به نام destination  می باشد که دارای پامتر های زیر است.
  </div>
  
  ```
 {
    "phone_number": "string",
    "reciver_name": "string",
    "province": "string",
    "city": "string",
    "floor": "string",
    "alley": "string",
    "street": "string",
    "plaque": "string",
    "latitude": "string",
    "longitude": "string"
 }
  ```
  
<div dir='rtl'>
زمانی که کاربر نحوه تحویل بسته (reciver_category)  را  ترمینال (port) انتخاب کند. شما باید ابتدا استان و شهر انتخاب شده کاربر را به آدرس زیر بفرستید و خروجی نمایش داده را دریافت کنید. خروجی زیر شامل  latitude و longitude ترمینال می باشد و پس از دریافت باید آن ها را درون destination قرار بدهید. 
  </div>
  
  ```
GET /api/v{version}/ports ?province={province}&countis={countis}
  ```
  
  **Output**
  
  ```
{
  "name": "قرچک",
  "province": "تهران ",
  "countis": "دماوند",
  "latitude": "35.6892",
  "longitude": "51.3890",
  "key": 1
}
  
  ```
  
  <div dir='rtl'>
  پارامتر های floor,alley, street, plaque,  دلبخواه می باشد و در این زمان نیازی به پر کردن آن ها نیست. 

</div>

<br>
<br>

<div dir='rtl'>
بیمه
</div>
<br>
<div dir='rtl'>
هنگام ثبت بسته یک گزینه برای بیمه شدن یا نشدن بسته وجود دارد که نام پارامتر آن is_insurance می باشد. زمانی کاربر گزینه بیشه شدن را تایید که باید یک رنج قیمتی برای این بسته ثبت شود که. برای این کار باید توسط آدرس زیر خروجی مورد نظر را دریافت کرده و سپس مقدار key دریافتی را درون insurance_value_key قرار دهید.
</div>

**API Address To Get insurance values**

```
get /api/v{version}/post-pack/insurance-values 
```

**Output**

```
{
  "items": [
    {
      "max": 200,
      "min": 100,
      "item": "بین 100 تا 200 میلیون تومان",
      "key": 1
    }
  ]
}
```
<div dir='rtl'>
 مقدار item را به کاربر نمایش دهید و بر اساس انتخاب آن key در insurance_value_key قرار بدید.
</div>

<div dir='rtl'>
توضیح خلاصه تمامی فیلد ها
</div>

```
{
  "content": "string",
  "description": "string",
  "pack_count": 0,               // تعداد بسته
  "is_packing": true,            // بسته بندی شود یا خیر
  "pay_at_origin": true,         // پرداخت در مبدا
  "is_insurance": true,          // آیا بیمه شود
  "insurance_value_key": 0,      // اگر بیمه بود کلید رنج قیمت آن را قراردهید  
  "pack_type_key": 0,            // نوع بسته 
  "reciver_category": "string",  // "port" or "destination"
  "package_value": "string",
  "weight_key": 0
}

```

<div dir='rtl'>

پس از این که پارامتر های مورد نظر را POST کردید و کد 201 دریافت کردید. حال لازم است سراغ مرحله تایید نهایی بسته برویم  و از آدرس زیر استفاده کنیم. بعد از ثبت بسته یک header به شما ارئه می شود که نام آن x-created-postpack-key می باید برای تایید بسته به آن نیاز داریم.
</div>

```
PUT /api/v{version}/post-pack/accept 
```

**Parameters**

```
{
  "string_post_pack_key": "string" 
  "pay_at_origin": true, // پرداخت در محل
  "is_cash_payment": true // نقدی بودن پرداخت
}
```

<div dir='rtl'>
مقدار  x-created-postpack-key را درون پارامتر string_post_pack_key قرار دهید.
</div>
