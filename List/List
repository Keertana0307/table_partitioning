CREATE DATABASE IF NOT EXISTS sales_partition_db;
USE sales_partition_db;

CREATE TABLE sales_list_partition (
    region VARCHAR(50) NOT NULL,
    country VARCHAR(50),
    item_type VARCHAR(50),
    sales_channel VARCHAR(20),
    order_priority CHAR(1),
    order_date DATE,
    order_id BIGINT,
    ship_date DATE,
    units_sold INT,
    unit_price DECIMAL(10,2)
) ENGINE = InnoDB
PARTITION BY LIST COLUMNS (region) (
    PARTITION p_europe VALUES IN ('EUROPE'),
    PARTITION p_na VALUES IN ('NORTH AMERICA'),
    PARTITION p_asia VALUES IN ('ASIA'),
    PARTITION p_mea VALUES IN ('MIDDLE EAST AND NORTH AFRICA'),
    PARTITION p_oceania VALUES IN ('AUSTRALIA AND OCEANIA')
);

ALTER TABLE sales_list_partition
ADD PARTITION (
    PARTITION p_other VALUES IN ('OTHER')
);


LOAD DATA INFILE
'C:/ProgramData/MySQL/MySQL Server 8.0/Uploads/sales_2021_2024_cleaned_upper.csv'
INTO TABLE sales_list_partition
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS
(region, country, item_type, sales_channel, order_priority,
 @order_date, order_id, @ship_date, units_sold, unit_price)
SET
order_date = STR_TO_DATE(@order_date, '%Y-%m-%d'),
ship_date  = STR_TO_DATE(@ship_date, '%Y-%m-%d');

-- Count total rows
SELECT COUNT(*) FROM sales_list_partition;

-- Check partition distribution
SELECT region, COUNT(*) AS cnt
FROM sales_list_partition
GROUP BY region;

-- Check partition pruning for a query
EXPLAIN
SELECT * FROM sales_list_partition
WHERE region = 'EUROPE';

--Create non-partition table for comparison
CREATE TABLE sales_non_partitioned (
    region VARCHAR(50) NOT NULL,
    country VARCHAR(50),
    item_type VARCHAR(50),
    sales_channel VARCHAR(20),
    order_priority CHAR(1),
    order_date DATE,
    order_id BIGINT,
    ship_date DATE,
    units_sold INT,
    unit_price DECIMAL(10,2)
);

LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 8.0/Uploads/sales_2021_2024_cleaned_upper.csv'
INTO TABLE sales_non_partitioned
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS
(region, country, item_type, sales_channel, order_priority,
 @order_date, order_id, @ship_date, units_sold, unit_price)
SET
order_date = STR_TO_DATE(@order_date, '%Y-%m-%d'),
ship_date  = STR_TO_DATE(@ship_date, '%Y-%m-%d');

SELECT * FROM sales_non_partitioned
WHERE region='EUROPE' AND order_date='2023-01-01' LIMIT 1;

–Create non partition database
CREATE DATABASE sales_non_partition;
USE sales_non_partition;
CREATE TABLE sales (
    region VARCHAR(50),
    country VARCHAR(50),
    item_type VARCHAR(50),
    sales_channel VARCHAR(20),
    order_priority CHAR(1),
    order_date DATE,
    order_id BIGINT,
    ship_date DATE,
    units_sold INT,
    unit_price DECIMAL(10,2)
);

LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 8.0/Uploads/sales_2021_2024_cleaned.csv'
INTO TABLE sales
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS
(region, country, item_type, sales_channel, order_priority,
 @order_date, order_id, @ship_date, units_sold, unit_price)
SET
order_date = STR_TO_DATE(@order_date, '%Y-%m-%d'),
ship_date  = STR_TO_DATE(@ship_date, '%Y-%m-%d');


SELECT COUNT(*) FROM sales_non_partition.sales;
SELECT COUNT(*) FROM sales_partition_db.sales_list_partition;








