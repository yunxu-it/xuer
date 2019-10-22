#### Room 数据库升级，增加新非空字段

```sqlite
Excepted:
paid=Column{name='paid', type='INTEGER', affinity='3', notNull=true, primaryKeyPosition=0, defaultValue='null'}

Found:
paid=Column{name='paid', type='INTEGER', affinity='3', notNull=false, primaryKeyPosition=0, defaultValue='null'}

// 解决办法：
新增字段时，添加默认值

private val migration_1_2: Migration = object : Migration(1, 2) {
      override fun migrate(database: SupportSQLiteDatabase) {
        database.execSQL("ALTER TABLE income " + " ADD COLUMN paid INTEGER NOT NULL default 1")
	}
}
```

