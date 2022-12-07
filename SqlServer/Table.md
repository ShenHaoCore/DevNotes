``` SQL
-- 将查询编辑器连接切换到 TestData 数据库
USE [TestData]
GO

-- 创建表
CREATE TABLE dbo.Products (
    ProductID INT IDENTITY(1, 1) PRIMARY KEY NOT NULL,
  	ProductKey UNIQUEIDENTIFIER NOT NULL,
    ProductName NVARCHAR(25) NOT NULL,
    Price DECIMAL(18, 2) NULL,
    ProductDescription VARCHAR(MAX) NULL
)
GO

-- 将数据插入到表
INSERT dbo.Products (ProductKey, ProductName, Price, ProductDescription)
    VALUES (NEWID(), 'Clamp', 12.48, 'Workbench clamp')
GO

-- 添加字段
ALTER TABLE dbo.Products ADD Price DECIMAL(18, 2) NULL
-- 修改字段
IF COL_LENGTH('Products', 'Price') IS NOT NULL -- 判断字段是否存在
BEGIN
		ALTER TABLE dbo.Products ALTER COLUMN Price DECIMAL(18, 2) NOT NULL
END

-- 添加字段说明
EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'字段说明内容', @level0type=N'SCHEMA', @level0name=N'dbo', @level1type=N'TABLE', @level1name=N'表名', @level2type=N'COLUMN', @level2name=N'列名'
-- 修改字段说明
EXEC sys.sp_updateextendedproperty @name=N'MS_Description', @value=N'字段说明内容', @level0type=N'SCHEMA', @level0name=N'dbo', @level1type=N'TABLE', @level1name=N'表名', @level2type=N'COLUMN', @level2name=N'列名'
```
