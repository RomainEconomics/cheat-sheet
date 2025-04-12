# PSQL Restore from pg_dump

Log as root and run this, knowing the dump file has been copy to the /tmp/ folder

```bash
k exec -n postgresql -it postgresql-0 -- psql -f /tmp/dump_file.pg_dump -U postgres
```
