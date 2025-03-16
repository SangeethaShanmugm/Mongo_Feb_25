mongostat => monitoring tools

C:\Program Files\MongoDB\Server\5.0\bin>mongostat

mongoexport
-----------

mongoexport --db feb_mongo25 --collection restaurant --out  A:\\mongodb_Data\\restaurantList.json

mongoimport --db mongo25 --collection restaurant --file  A:\\mongodb_Data\\restaurantList.json

mongodump -o A:\\mongodb_Data\\dumpData --db mongo25 -c restaurant