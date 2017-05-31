-- names of chefs who do not prepare pasta
select distinct name from
(
  select preps.cid, preps.did, chef.name from
  (
    preps
    join chef on preps.cid = chef.cid
  )join dish on dish.did = preps.did and dish.name != "pasta"
);

-- names of dishes prepared by only 1 chef

select name from(
  select preps.cid, preps.did, name, count(*) as c from preps join(
    select did as ddid, name from dish)
  where preps.did = ddid group by name
)where c = 1;

-- above average chefs

select name, cid from
(
  select * from chef join(select avg(rating) as a from chef)
  where rating > a
);

-- above average dish

select name, did from
(
  select * from dish join(select avg(popularity) as p from dish)
  where popularity > p
);

-- above average chefs with above average dishes

select cname, dname from
(
  select * from
  (
    (select ccid, cname, preps.did, preps.cid from preps join(select name as cname, cid as ccid from (
      select * from chef join(select avg(rating) as a from chef) where rating > a)) on preps.cid = ccid)
    join
    (select name as dname, did as ddid from (
      select * from dish join(select avg(popularity) as p from dish) where popularity > p))
    on ddid = did
  )
);

-- chef c000 longer prepares pasta --

delete from preps where cid is 100 and did is 100;

-- schema def --

CREATE TABLE chef
(
  cid integer,
  name varchar,
  rating float,

  primary key(cid)
);

CREATE TABLE dish
(
  did integer,
  name varchar,
  popularity float,

  primary key(did)
);

CREATE TABLE preps
(
  cid integer,
  did integer,

  primary key(cid, did)
);

insert into chef values(100, "c000", 4.0001); -- above avg
insert into chef values(200, "c111", 3.5001); -- above avg
insert into chef values(300, "c222", 2.2001);
insert into chef values(400, "c333", 2.2001);
insert into chef values(500, "c444", 4.4001); -- above avg

insert into dish values(100, "pasta", 2.001);
insert into dish values(200, "steak", 4.101); -- above avg
insert into dish values(300, "curry", 3.501); -- above avg
insert into dish values(400, "brats", 3.901); -- above avg
insert into dish values(500, "eggos", 1.901);

insert into preps values(100, 100);
insert into preps values(200, 100);
insert into preps values(300, 200);
insert into preps values(300, 300);
insert into preps values(400, 400);
insert into preps values(500, 400); -- top chef
insert into preps values(500, 200); -- top chef
insert into preps values(500, 500); -- top chef
