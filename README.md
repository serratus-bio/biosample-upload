## Lambda setup

- run `create-layer.sh` on AWS CloudShell

## SQL

```sql
ALTER TABLE biosample ADD PRIMARY KEY (biosample_id);
```

some interesting queries:

```sql
select count(*) from biosample
where lat_lon is not null or geo_loc_name is not null

select count(distinct geo_loc_name) from biosample

select geo_loc_name, count(*) from biosample
group by geo_loc_name
limit 100
```

## unzip to s3

```sh
# copy biosample_set.xml.gz
wget -qO- https://ftp.ncbi.nlm.nih.gov/biosample/biosample_set.xml.gz | aws s3 cp - s3://serratus-public/notebook/210212_geo/victorlin/biosample_parse/biosample_set.xml.gz

# unzip to biosample_set.xml
aws s3 cp s3://serratus-public/notebook/210212_geo/victorlin/biosample_parse/biosample_set.xml.gz - | zcat | aws s3 cp - s3://serratus-public/notebook/210212_geo/victorlin/biosample_parse/biosample_set.xml
```

## head

```bsh
zcat < biosample_set.xml.gz | head -n 100000 > head.xml
```
