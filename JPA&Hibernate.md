# Important-Notes

## Hibernate
It is the implementation of JpaRepository interface which provide ways to perform ORM operations. The order of operations are:
SessionFactory is created >> Session object is returned By Session Factory >> Transaction is started >> DB operations are performed using session object >> Transaction is committed or rollbacked (Once all transactions are successful or failed) >> Session is closed (To release the resources)

Hibernate is better because of better TransactionManagement,  Session (Entity in case of JPA) Life Cycle, Caching.

Hibernate has got two level caching 1). First-Level Cache: It is by default there and cannot be closed, internally it caches data in the persistence context and It is unique for particular session and never shared among sessions 2). Second-Level Cache : shared cache across multiple sessions
Session has persistence context which actually caches the data. 

### Difference between JPA and Hibernate
In JPA to manage sessions, we have got EntityManagerFactory which returns entity manager which manages entity. For Transaction management, It has platform transaction management. 
In Hibernate, we have got SessionManagerFactory which returns session object and we perform all the operations on this session object. We can create multiple sessionmanager factory for multiple databases and can use their session object accordingly.
In Hibernate, for creating configuration file we create hibernate.cfg.xml and for creating mapping between class and table, we create class_name.hbm.xml
In JPA, these xml files get replaced by annotations. 
@OneToMany and @ManyToMany associations use the FetchType.LAZY strategy.
@OneToOne and @ManyToOne use the FetchType.EAGER strategy

https://github.com/in28minutes/jpa-with-hibernate
