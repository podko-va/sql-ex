WITH DateRange AS (
  SELECT CAST('2003-04-01' AS DATETIME) AS date
  UNION ALL
  SELECT DATEADD(day, 1, date)
  FROM DateRange
  WHERE date < '2003-04-07'
)
SELECT 
    d.date,
    COALESCE(b.Qty, 0) as Qty
FROM DateRange d
LEFT JOIN (
    SELECT 
        p.date,
        COUNT(DISTINCT t.trip_no) as Qty
    FROM Pass_in_trip p
    INNER JOIN Trip t 
        ON t.trip_no = p.trip_no 
        AND t.town_from = 'Rostov'
    WHERE p.date BETWEEN '2003-04-01' AND '2003-04-07'
    GROUP BY p.date
) b ON d.date = b.date
OPTION (MAXRECURSION 7);
