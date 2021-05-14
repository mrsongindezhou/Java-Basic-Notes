## 数据库设计三大范式
范式：指对数据库优化数据存储方式的规范，在关系型数据库中这些规范称为范式。
#### 1．第一范式(确保每列保持原子性)

- 1NF是最基本的范式。
- 每一列属性都是不可再分的属性值，保证每一列的原子性；
- 两列的属性相近或相似或一样，尽量合并属性一样的列，确保不产生冗余数据；

#### 2．第二范式(确保表中的每列都和主键相关)
- 如果关系模式R满足第一范式，并且R的所有非主属性都完全依赖于R的每一个候选关键属性，称R满足第二范式，记为2NF；
- 每一行的数据只能与其中一列相关，即一行数据只做一件事；只有数据列中出现数据重复，就要把表拆分开。



#### 3．第三范式(确保每列都和主键列直接相关,而不是间接相关)
- 数据不能存在传递关系，即每个属性都跟主键有直接关系而不是间接关系。
- 3NF是对字段的**冗余性**，要求任何字段不能由其他字段派生出来，它要求字段没有冗余，即不存在传递依赖；


#### 4. 反范式化

- 反范式化： 有时为了提高运行效率，就必须降低范式标准，适当保留冗余数据。
- 具体做法是：在概念数据模型设计时遵守第三范式，降低范式标准的工作放到物理数据模型设计时考虑。降低范式就是增加字段，允许冗余，达到以空间换时间的目的。


#### 5. 范式化设计和反范式化设计的优缺点

##### 5.1 范式化 （时间换空间）

- 优点：
范式化的表减少了数据冗余，数据表更新操作快、占用存储空间少。
- 缺点：
查询时需要对多个表进行关联，查询性能降低。
更难进行索引优化。

##### 5.2 反范式化（空间换时间）

反范式的过程就是通过冗余数据来提高查询性能，但冗余数据会牺牲数据一致性
###### 优点：
- 可以减少表关联
- 可以更好进行索引优化

###### 缺点：
- 存在大量冗余数据
- 数据维护成本更高（删除异常，插入异常，更新异常）
