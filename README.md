# database_checkpoint

## CHALLENGE 1

Query:
```SQL
SELECT * FROM destinations;
```
Results:
```
vacations=# SELECT * FROM destinations;

 id |       name       | average_temp | has_beaches | has_mountains | cost_of_flight
----+------------------+--------------+-------------+---------------+----------------
  1 | Thailand         |           82 | t           | t             |            765
  2 | Minnesota        |           41 | f           | f             |            235
  3 | New Zealand      |           66 | t           | t             |            433
  4 | England          |           45 | f           | f             |            290
  5 | Tristan da Cunha |           59 | t           | t             |           1304
(5 rows)
```

## CHALLENGE 2

Query:
```SQL
SELECT * FROM destinations WHERE has_beaches = 'true';
```
Results:
```
vacations=# SELECT * FROM destinations WHERE has_beaches = 'true';

 id |       name       | average_temp | has_beaches | has_mountains | cost_of_flight
----+------------------+--------------+-------------+---------------+----------------
  1 | Thailand         |           82 | t           | t             |            765
  3 | New Zealand      |           66 | t           | t             |            433
  5 | Tristan da Cunha |           59 | t           | t             |           1304
(3 rows)
```

## CHALLENGE 3

Query:
```SQL
SELECT * FROM destinations WHERE average_temp > 60;
```
Results:
```
vacations=# SELECT * FROM destinations WHERE average_temp > 60;

 id |    name     | average_temp | has_beaches | has_mountains | cost_of_flight
----+-------------+--------------+-------------+---------------+----------------
  1 | Thailand    |           82 | t           | t             |            765
  3 | New Zealand |           66 | t           | t             |            433
(2 rows
```

## CHALLENGE 4

Query:
```SQL
SELECT * FROM destinations WHERE has_beaches ='true' AND has_mountains='true';
```
Results:
```
vacations=# SELECT * FROM destinations where has_beaches ='true' AND has_mountains='true';

 id |       name       | average_temp | has_beaches | has_mountains | cost_of_flight
----+------------------+--------------+-------------+---------------+----------------
  1 | Thailand         |           82 | t           | t             |            765
  3 | New Zealand      |           66 | t           | t             |            433
  5 | Tristan da Cunha |           59 | t           | t             |           1304
(3 rows)
```

## CHALLENGE 5

Query:
```SQL
SELECT * FROM destinations WHERE cost_of_flight < 500;
```
Results:
```
vacations=# SELECT * FROM destinations WHERE cost_of_flight < 500;

 id |    name     | average_temp | has_beaches | has_mountains | cost_of_flight
----+-------------+--------------+-------------+---------------+----------------
  2 | Minnesota   |           41 | f           | f             |            235
  3 | New Zealand |           66 | t           | t             |            433
  4 | England     |           45 | f           | f             |            290
(3 rows)
```

## CHALLENGE 6

Query:
```SQL
INSERT INTO destinations VALUES (6, 'The Bahamas',78,true,false,345);
```
Results:
```
vacations=# INSERT INTO destinations VALUES (6, 'The Bahamas',78,true,false,345);
INSERT 0 1

vacations=# select * from destinations;

 id |       name       | average_temp | has_beaches | has_mountains | cost_of_flight
----+------------------+--------------+-------------+---------------+----------------
  1 | Thailand         |           82 | t           | t             |            765
  2 | Minnesota        |           41 | f           | f             |            235
  3 | New Zealand      |           66 | t           | t             |            433
  4 | England          |           45 | f           | f             |            290
  5 | Tristan da Cunha |           59 | t           | t             |           1304
  6 | The Bahamas      |           78 | t           | f             |            345
(6 rows)
```

## CHALLENGE 7

Query:
```SQL
UPDATE destinations SET cost_of_flight = 1000 WHERE id = 3;
```
Results:
```
vacations=# UPDATE destinations SET cost_of_flight = 1000 WHERE id = 3;
UPDATE 1

vacations=# select * from destinations;

 id |       name       | average_temp | has_beaches | has_mountains | cost_of_flight
----+------------------+--------------+-------------+---------------+----------------
  1 | Thailand         |           82 | t           | t             |            765
  2 | Minnesota        |           41 | f           | f             |            235
  4 | England          |           45 | f           | f             |            290
  5 | Tristan da Cunha |           59 | t           | t             |           1304
  6 | The Bahamas      |           78 | t           | f             |            345
  3 | New Zealand      |           66 | t           | t             |           1000
(6 rows)
```

## CHALLENGE 8
Query:
```SQL
DELETE FROM destinations WHERE id = 2 RETURNING *;
```
Results:
```
vacations=# DELETE FROM destinations WHERE id = 2;
DELETE 1

vacations=# select * from destinations;

 id |       name       | average_temp | has_beaches | has_mountains | cost_of_flight
----+------------------+--------------+-------------+---------------+----------------
  1 | Thailand         |           82 | t           | t             |            765
  4 | England          |           45 | f           | f             |            290
  5 | Tristan da Cunha |           59 | t           | t             |           1304
  6 | The Bahamas      |           78 | t           | f             |            345
  3 | New Zealand      |           66 | t           | t             |           1000
(5 rows)
```

## CHALLENGE 9
Query:
```SQL
UPDATE destinations SET name = 'Scotland' WHERE name = 'England';
```
Results:
```
vacations=# UPDATE destinations SET name = 'Scotland' WHERE name = 'England';
UPDATE 1

vacations=# select * from destinations;

 id |       name       | average_temp | has_beaches | has_mountains | cost_of_flight
----+------------------+--------------+-------------+---------------+----------------
  1 | Thailand         |           82 | t           | t             |            765
  5 | Tristan da Cunha |           59 | t           | t             |           1304
  3 | New Zealand      |           66 | t           | t             |           1000
  6 | The Bahamas      |           78 | t           | f             |            345
  4 | Scotland         |           45 | f           | f             |            290
(5 rows)
```

## CHALLENGE 10

Query:
```SQL
ALTER TABLE airlines ADD PRIMARY KEY (id);

ALTER TABLE destinations ADD PRIMARY KEY (id);

CREATE TABLE airlines_destinations (
 id SERIAL,
 PRIMARY KEY (id),
 airline_id integer,
 CONSTRAINT fk_airlines
 FOREIGN KEY (airline_id)
 REFERENCES airlines(id),
 destinations_id integer,
 CONSTRAINT fk_destinations
   FOREIGN KEY (destinations_id)
    REFERENCES destinations(id)
);

INSERT INTO airlines_destinations (airline_id, destinations_id)
VALUES
(1,3),
(1,4),
(2,5),
(2,4),
(2,1),
(3,1),
(3,4),
(4,3),
(4,5);
```
Results:
```
vacations=# ALTER TABLE destinations ADD PRIMARY KEY (id);
ALTER TABLE

vacations=# \d destinations

                                      Table "public.destinations"
     Column     |         Type          | Collation | Nullable |                Default
----------------+-----------------------+-----------+----------+---------------------------------------
 id             | integer               |           | not null | nextval('vacations_id_seq'::regclass)
 name           | character varying(50) |           |          |
 average_temp   | integer               |           |          |
 has_beaches    | boolean               |           |          |
 has_mountains  | boolean               |           |          |
 cost_of_flight | integer               |           |          |
Indexes:
    "destinations_pkey" PRIMARY KEY, btree (id)

vacations=# ALTER TABLE airlines ADD PRIMARY KEY (id);
ALTER TABLE

vacations=# \d airlines

                                   Table "public.airlines"
 Column |         Type          | Collation | Nullable |               Default
--------+-----------------------+-----------+----------+--------------------------------------
 id     | integer               |           | not null | nextval('airlines_id_seq'::regclass)
 name   | character varying(50) |           |          |
Indexes:
    "airlines_pkey" PRIMARY KEY, btree (id)

vacations=# CREATE TABLE airlines_destinations (
 id SERIAL,
 PRIMARY KEY (id),
 airline_id integer,
 CONSTRAINT fk_airlines
 FOREIGN KEY (airline_id)
 REFERENCES airlines(id),
 destinations_id integer,
 CONSTRAINT fk_destinations
   FOREIGN KEY (destinations_id)
    REFERENCES destinations(id)
);
CREATE TABLE

vacations=# \d airlines_destinations

                                 Table "public.airlines_destinations"
     Column      |  Type   | Collation | Nullable |                      Default
-----------------+---------+-----------+----------+---------------------------------------------------
 id              | integer |           | not null | nextval('airlines_destinations_id_seq'::regclass)
 airline_id      | integer |           |          |
 destinations_id | integer |           |          |
Indexes:
    "airlines_destinations_pkey" PRIMARY KEY, btree (id)
Foreign-key constraints:
    "fk_airlines" FOREIGN KEY (airline_id) REFERENCES airlines(id)
    "fk_destinations" FOREIGN KEY (destinations_id) REFERENCES destinations(id)

vacations=# INSERT INTO airlines_destinations (airline_id, destinations_id)
vacations-# VALUES
vacations-# (1,3),
vacations-# (1,4),
vacations-# (2,5),
vacations-# (2,4),
vacations-# (2,1),
vacations-# (3,1),
vacations-# (3,4),
vacations-# (4,3),
vacations-# (4,5);
INSERT 0 9

vacations=# select * from airlines_destinations;

 id | airline_id | destinations_id
----+------------+-----------------
  1 |          1 |               3
  2 |          1 |               4
  3 |          2 |               5
  4 |          2 |               4
  5 |          2 |               1
  6 |          3 |               1
  7 |          3 |               4
  8 |          4 |               3
  9 |          4 |               5
(9 rows)
```

## CHALLENGE 11

Query:
```SQL
SELECT airlines.name FROM airlines WHERE airlines.id IN (SELECT airline_id FROM airlines_destinations WHERE airlines_destinations.destinations_id=3);
```
Results:
```
vacations=# SELECT airlines.name FROM airlines WHERE airlines.id IN (SELECT airline_id FROM airlines_destinations WHERE airlines_destinations.destinations_id=3);

   name
-----------
 Spirit
 SouthWest
(2 rows)
```

## CHALLENGE 12

Query:
```SQL
SELECT airlines.name FROM airlines WHERE airlines.id NOT IN (SELECT airline_id FROM airlines_destinations WHERE airlines_destinations.destinations_id=4);
```
Results:
```
vacations=# SELECT airlines.name FROM airlines WHERE airlines.id NOT IN (SELECT airline_id FROM airlines_destinations WHERE airlines_destinations.destinations_id=4);

   name
-----------
 SouthWest
(1 row)
```

## CHALLENGE 13

Query:
```SQL
SELECT * FROM destinations;
```
Results:
```
vacations=# SELECT * FROM destinations;

 id |       name       | average_temp | has_beaches | has_mountains | cost_of_flight
----+------------------+--------------+-------------+---------------+----------------
  1 | Thailand         |           82 | t           | t             |            765
  5 | Tristan da Cunha |           59 | t           | t             |           1304
  3 | New Zealand      |           66 | t           | t             |           1000
  6 | The Bahamas      |           78 | t           | f             |            345
  4 | Scotland         |           45 | f           | f             |            290
(5 rows)
```