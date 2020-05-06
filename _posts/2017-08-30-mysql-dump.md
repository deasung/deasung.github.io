---

title: MYSQL DUMP 뜨고 삽입
published: true
---


```
BACKUP_DATE=$(date +%Y%m%d)
BACKUP_PATH="/home/zipdockr/backup/DB"
DELETE_DATE=$(date -d '10 day ago' +%Y%m%d)
DELETE_FILE="$BACKUP_PATH/zipdockr_$DELETE_DATE.sql.gz"
echo "backup start : $BACKUP_DATE"

cd ~/backup/DB
mysqldump -uzipdockr -p'zipdoc!@#' zipdockr | gzip > zipdockr_$BACKUP_DATE.sql.gz

echo "backup end : $BACKUP_DATE"
echo "delete start : $DELETE_FILE"

if [ -f "$DELETE_FILE" ]; then
echo "file exist"
rm $DELETE_FILE
fi

```
