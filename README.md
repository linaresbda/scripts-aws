# aws

## RDS
  ### Importar/Exportar base de datos
  
  *IMPORTAR BASE DE DATOS  (el archivo de restauracion debe de estar publico para se tenga a exceso desde el exterior)*
  ```[sql]
    exec msdb.dbo.rds_restore_database
     @restore_db_name='{{namedb}}',
     @s3_arn_to_restore_from='arn:aws:s3:::{{bucketname}}/{{filename}}.bak';
  ```
    
  *EXPORTAR BASE DE DATOS  (El bucket debe de tener acceso publico para que se pueda almacenar el archivo de restauracion)*
  ```[sql]
    exec msdb.dbo.rds_backup_database
      @source_db_name='{{namedb}}',
      @s3_arn_to_backup_to='arn:aws:s3:::{{bucketname}}/{{filename}}.bak',
      @overwrite_S3_backup_file=1,
      @type='full';
  ```
  
  *Comando para conocer el estatus del proceso Importar/Exportar*

  ```[sql]
      exec msdb.dbo.rds_task_status
  ```
  
*IMPORTANTE: Al final de cada IMPORTACION o EXPORTACION cambiar los accesos de publicos a privados del repo(bucket) en Amazon*
