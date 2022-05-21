
# JPa

## Get list of managed classes in given EntityManager

```java
Set<EntityType<?>> set = em.getMetamodel().getEntities();
```

## Get list of Entity annotated class with Reflections

```java
org.reflections.Reflections reflections = new org.reflections.Reflections("it.sisnet");
Set<Class<?>> set = reflections.getTypesAnnotatedWith(javax.persistence.Entity.class);
```


