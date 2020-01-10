# Presto


> url : https://presto-online.barongpos.com/api

# API FB 
**outlet** = rst, msc <br>
**dept** = nama_dept seperti CHRISPY PIZZA <br>
**type** = Food dan beverage <br>

## Report Overview
    Route::get('homeFb/{outlet}', 'Api\HomeController@indexFb'); // date dan dept
    ## homeFb [/homeFb/{outlet}?date=:date&dept=:dept]
    {outlet} = menggunakan kode out => RST dan MSC 
    {date} = 2019-12-30
    {dept} = nama dept => CRISPY PIZZA
> http://localhost/PRESTO/public/api/homeFb/RST?date=2020-01-01&dept=CRISPY+PIZZA


## Report Payment
    Route::get('paymentFb/{outlet}', 'Api\HomeController@paymentFb'); // date dan dept
    ## paymentFb [/paymentFb/{outlet}?date=:date&dept=:dept]
    {outlet} = menggunakan kode out => RST dan MSC
    {date} = 2019-12-30
    {dept} = nama dept => CRISPY PIZZA
> http://localhost/PRESTO/public/api/paymentFb/RST?date=2019-11-20&dept=CRISPY+KROBOKAN



## Top 10 Product sales (yg dari APP PHIS)
    Route::get('productSales/{type}/{outlet}', 'Api\HomeController@productSales'); // ok, ditambah date dan dept
    ## productSales [/productSales/{type}/{outlet}?date=:date&dept=:dept]
    {type} = menggunakan food atau beverage, 
    {outlet} = menggunakan kode out => RST dan MSC
    {date} = 2019-12-30
    {dept} = nama dept => CRISPY PIZZA
> http://localhost/PRESTO/public/api/productSales/food/rst?date=2019-06-22&dept=CRISPY+PIZZA


## Report Transaction summary (by APP)
    Route::get('transactionSummary/{outlet}', 'Api\HomeController@transactionSummary'); // date dan dept
    ## transactionSummary [/transactionSummary/{outlet}?date=:date&dept=:dept]
    {outlet} = menggunakan kode out => RST dan MSC 
    {date} = 2019-12-30
    {dept} = nama dept => CRISPY PIZZA
> http://localhost/PRESTO/public/api/transactionSummary/RST?date=2019-11-25&dept=CRISPY+PIZZA

## Sales Performance
    Route::get('salesPerformance/{outlet}', 'Api\HomeController@salesPerformance'); // date dan dept
    ## salesPerformance [/salesPerformance/{outlet}?date=:date&dept=:dept]
    {outlet} = menggunakan kode out => RST dan MSC 
    {date} = 2019-12-30
    {dept} = nama dept [gross]
> http://localhost/PRESTO/public/api/salesPerformance/RST?date=2019-11-25&dept=CRISPY+PIZZA


## Sales Trafic
    Route::get('salesTrafic/{outlet}', 'Api\HomeController@salesTrafic'); // date dan dept
    ## salesTrafic [/salesTrafic/{outlet}?date=:date&dept=:dept]
    {outlet} = menggunakan kode out => RST dan MSC 
    {date} = 2019-12-30
    {dept} = nama dept [gross]
> http://localhost/PRESTO/public/api/salesTrafic/RST?date=2019-11-25&dept=CRISPY+PIZZA

## Outlets
    Route::get('getOutlets', 'Api\HomeController@getOutlets');
    ## Get Outlets [/getOutlets]
> http://localhost/PRESTO/public/api/getOutlets
```json
    [
        {
            "kode_out": "MSC",
            "nama_out": "MISCELLANEOUS"
        },
        {
            "kode_out": "RST",
            "nama_out": "RESTAURANT"
        },
        {
            "kode_out": "all",
            "nama_out": "All Outlet"
        }
    ]
```
## Departement
    Route::get('getDept', 'Api\HomeController@getDept');
    ## getDept [/getDept]
> http://localhost/PRESTO/public/api/getDept
```json
    [
        {
            "nama_dept": "CRISPY PIZZA",
            "unit_bisnis": "CRISPY PIZZA"
        },
        {
            "nama_dept": "CRISPY KROBOKAN",
            "unit_bisnis": "CRISPY PIZZA"
        },
        {
            "nama_dept": "CRISPY BANDUNG",
            "unit_bisnis": "CRISPY PIZZA"
        },
    ]
```

# Baru (Dashboard PRESTO)
{date} = 2019-12-30,

{outlet} = dari form input setOutlet, menggunakan nama_dept => CHRISPY PIZZA
    {dept} = dari form input setOutlet, menggunakan nama_dept => CHRISPY PIZZA

{tipe} = khusus setiap url
{type} = food, beverage

{jenis_outlet} =  rst atau msc
    {outlet} =  rst atau msc

## Sales Performance Outlet
    Route::get('/ajaxBestOutlet', ['as' => 'ajax.best.outlet', 'uses' => 'Api\HomeController@ajaxBestOutlet']);
    ## ajaxBestOutlet [/ajaxBestOutlet?date=:date&outlet=:outlet&tipe=:tipe]
    {date} = 2019-12-30,
    {outlet} = dari form input setOutlet, menggunakan nama_dept => CHRISPY PIZZA
            merubah parameter {outlet} menjadi {dept}
    {tipe} = ('WTD', 'YTD', 'MTD') default 'YTD' [total gross] //--------- khusus ---------//
    
    http://localhost/PRESTO/public/api/ajaxBestOutlet?date=2019-11-28&outlet=all&tipe=YTD

> http://localhost/PRESTO/public/api/ajaxBestOutlet?date=2019-11-28&dept=CRISPY+KROBOKAN&tipe=YTD


## top ten sales by product
    Route::get('/ajaxSellProduct', ['as' => 'ajax.sell.product', 'uses' => 'Api\HomeController@ajaxSellProduct']);
    ## ajaxSellProduct [/ajaxSellProduct?date=:date&outlet=:outlet&tipe=:tipe]
    {date} = 2019-12-30
    {outlet} = dari form input setOutlet, menggunakan nama_dept => CHRISPY PIZZA
            merubah parameter {outlet} menjadi {dept}
    {tipe} = ('DTD', 'MTD', 'YTD') default 'DTD' //--------- khusus ---------//
    {type} = food, beverage
    {jenis_outlet} =  (rst atau msc) default all
            merubah parameter {jenis_outlet} menjadi {outlet}
    lama : http://localhost/PRESTO/public/api/ajaxSellProduct?type=food&date=2019-11-28&outlet=CRISPY PIZZA&tipe=YTD&jenis_outlet=msc
> http://localhost/PRESTO/public/api/ajaxSellProduct?type=food&date=2019-11-28&dept=CRISPY+PIZZA&tipe=YTD&outlet=rst


## report analisys by time order
    Route::get('/ajaxAnalisisByTime', ['as' => 'ajax.sales.time', 'uses' => 'Api\HomeController@analisysByTime']);
    ## ajaxAnalisisByTime [/ajaxAnalisisByTime?date=:date&outlet=:outlet&tipe=:tipe]
    {date} = 2019-12-30,
    {outlet} = dari form input setOutlet, menggunakan nama_dept => CHRISPY PIZZA
            merubah parameter {outlet} menjadi {dept}
    {tipe} = ('MTD', 'DTD') default 'MTD' //--------- khusus ---------//
    lama : http://localhost/PRESTO/public/api/ajaxAnalisisByTime?date=2019-11-20&outlet=CRISPY_KROBOKAN&tipe=MTD
> http://localhost/PRESTO/public/api/ajaxAnalisisByTime?date=2019-11-20&dept=CRISPY+KROBOKAN&tipe=MTD


## report average bill net per pax
    Route::get('/ajaxAnalisisAverage', ['as' => 'ajax.sales.average', 'uses' => 'Api\HomeController@ajaxSalesAverage']);
    ## ajaxAnalisisAverage [/ajaxAnalisisAverage?date=:date&outlet=:outlet&tipe=:tipe]
    {date} = 2019-12-30
    {outlet} = dari form input setOutlet, menggunakan nama_dept => CHRISPY PIZZA
            merubah parameter {outlet} menjadi {dept}
    {tipe} = ('YTD', 'DTD') default 'YTD' //--------- khusus ---------//
    lama : http://localhost/PRESTO/public/api/ajaxAnalisisAverage?date=2019-11-12&outlet=CRISPY BANDUNG&tipe=YTD
> http://localhost/PRESTO/public/api/ajaxAnalisisAverage?date=2019-11-12&dept=CRISPY+BANDUNG&tipe=YTD


# DRR

office = rst, msc <br>
TyPE = Food dan beverage <br>
date = 2019-12-30 <br>
setOutlet = nama_dept seperti CHRISPY PIZZA <br>
outlet = nama_dept seperti CHRISPY PIZZA <br>


Diganti menjadi <br>
dept = nama_dept seperti CHRISPY PIZZA <br>
outlet = rst, msc <br>

## DRR
    Route::get('reportDailyRevenue', 'Api\HomeController@dailyRevenue');
    ## reportDailyRevenue [/reportDailyRevenue?date=:date&office=:office&outlet=:outlet]
    {date} = 2019-12-30
    {office} = menggunakan kode_out => rst, msc
            merubah parameter {office} menjadi {outlet}
    {outlet} = menggunakan nama_dept => CHRISPY PIZZA
            merubah parameter {outlet} menjadi {dept}
    // dirubah pada ReportRepositoryApi
    lama : http://localhost/PRESTO/public/api/reportDailyRevenue?date=2019-11-25&office=RST&outlet=CRISPY+PIZZA
    
> http://localhost/PRESTO/public/api/reportDailyRevenue?date=2019-11-25&outlet=RST&dept=CRISPY+PIZZA

## Report Product favorite
    Route::get('reportProductFav', 'Api\HomeController@reportProductFav')->name('report.product.fav'); // F
    ## reportProductFav [/reportProductFav?date=:date&outlet=:outlet]
    {date} = 2019-12-30
    {outlet} = menggunakan nama_dept => CHRISPY PIZZA
            merubah parameter {outlet} menjadi {dept}
    lama : http://localhost/PRESTO/public/api/reportProductFav?date=2019-11-20&outlet=CRISPY PIZZA

> http://localhost/PRESTO/public/api/reportProductFav?date=2019-11-20&dept=CRISPY+PIZZA
 
## report analisis by day (sunday, monday dll)
    Route::get('reportKasir', 'Api\HomeController@reportKasir')->name('report.kasir');
    ## reportKasir [/reportKasir?date=:date&setOutlet=:setOutlet]
    {date} = 2019-12-30,
    {setOutlet} = menggunakan nama_dept => CHRISPY PIZZA
            merubah parameter {setOutlet} menjadi {dept}
    lama : http://localhost/PRESTO/public/api/reportKasir?date=2019-11-25&setOutlet=CRISPY BANDUNG

> http://localhost/PRESTO/public/api/reportKasir?date=2019-11-25&dept=CRISPY+BANDUNG


# PROCEDURE 



BEGIN

    DECLARE p_outlet varchar(191);
    DECLARE p_dept varchar(191);

SELECT bill.nobill, bill.tanggal, bill.net, bill.kode_pro as bill_produk, TRIM(produk.groups) as group_produk, bill.disc_nom as diskon, listbill.compliment, listbill.net as listbill_net, listbill.pax, bill.gross, bill.tax, bill.ser, listbill.cash, listbill.cc as cc1, listbill.cc2, listbill.other AS arNominal, listbill.gb as chargeToRoom, listbill.cash_usd as foreign_cash, listbill.forex, listbill.voucher as voucherPromo, listbill.deposit as clearingDp, listbill.free_bf as voucherBf, listbill.tip as guestTiping, bill.compli, listbill.total as totalListbill, listbill.cdept as dept2

FROM bill

INNER JOIN produk ON bill.kode_pro=produk.kode_pro
INNER JOIN listbill ON bill.nobill=listbill.nobill

WHERE bill.tanggal = pdate AND listbill.cdept = pdept AND bill.kode_out = poutlet;

    IF poutlet != 'all' THEN
        SET p_outlet = 'AND bill.kode_out = poutlet';
    ELSE
        SET p_outlet = '';
    END IF;

END
