# Stream的使用

```java
        //创建一些数据
        List<User> list = new ArrayList<>();
        User user = new User(1, "a", "小明");
        User user1 = new User(2, "a", "小红");
        User user2 = new User(3, "b", "小李");
        User user3 = new User(4, "a", "小红");
        list.add(user);
        list.add(user1);
        list.add(user2);
        list.add(user3);

        //创建stream流的方式
        Stream<User> stream = list.stream();
        Stream<User> stringStream = list.parallelStream();

        //将多个User转换为Stream
        User[] users = new User[2];
        Stream<User> stream1 = Arrays.stream(users);
        //将数组转换为Stream
        Stream<String> stream4 = Stream.of("11", "2");

        group(list);

        convertTo(list);

        //字符拼接
        List<String> stringList = Arrays.asList("a", "b", "c");
        String appendString = stringList.stream().collect(Collectors.joining(","));
        System.out.println("-----------字符拼接------------");
        System.out.println(appendString);

        //排序
        List<User> compar = list.stream().sorted(Comparator.comparing(User::getType)).collect(Collectors.toList());
        System.out.println("-----------排序------------");
        System.out.println(compar);

        //总数
        Long count = list.stream().collect(Collectors.counting());
        System.out.println("-----------总数------------");
        System.out.println(count);

        //循环遍历
        System.out.println("-----------循环遍历------------");
        list.stream().forEach(System.out::println);

        maxormin(list);

        //筛选
        List<User> list1 = list.stream().filter(x -> x.getId() > 1).collect(Collectors.toList());
        System.out.println("-------------筛选-------------");
        System.out.println(list1);

        //匹配
        boolean b = list.stream().anyMatch(x -> x.getType().equals("b"));
        boolean b1 = list.stream().allMatch(x -> x.getType().equals("b"));
        boolean b2 = list.stream().noneMatch(x -> x.getType().equals("b"));
        System.out.println("----------------匹配--------------");
        System.out.println("anyMatch:" + b);
        System.out.println("allMatch:" + b1);
        System.out.println("noneMatch:" + b2);

        //去重
        System.out.println("-----------去重------------");
        List<String> strings = Arrays.asList("a", "b", "c", "a");
        strings.stream().distinct().forEach(System.out::println);

        //截断流Limit,使其元素不超过给定数量
        List<String> limit = strings.stream().limit(2L).collect(Collectors.toList());
        System.out.println("--------------截断流--------------");
        System.out.println(limit);

        //映射 Stream中包含5个映射方法：map、mapToDouble、mapToInt、mapToLong和flatMap
        List<String> nameList = list.stream().map(User::getName).collect(Collectors.toList());
        BigDecimal sum = users.stream().map(User::getCj).reduce(BigDecimal.ZERO, BigDecimal::add)
        System.out.println("--------------映射----------------");
        System.out.println(nameList);

 /**
     * 取最大最小值
     * @param list
     */
    private void maxormin(List<User> list) {
        //取最大值
        User user4 = list.stream().max(Comparator.comparing(User::getId)).get();
        System.out.println("-------------取集合中Id最大的User-------------");
        System.out.println(user4);
        Integer max = list.stream().map(x -> x.getId()).max(Integer::compareTo).get();
        System.out.println("----------------取出User集合中最大的id------------------");
        System.out.println(max);

        //取最小值
        User user5 = list.stream().min((u1, u2) -> u1.getId().compareTo(u2.getId())).get();
        System.out.println("-------------取集合中Id最小的User-------------");
        System.out.println(user5);

        //取平均值
        Double average = list.stream().collect(Collectors.averagingInt(User::getId));
        System.out.println("-------------取平均值-------------");
        System.out.println(average);
    }

    /**
     * 转换
     *
     * @param list
     */
    private void convertTo(List<User> list) {
        //Stream转换list set
        String[] testStrings = {"a", "b", "c", "d", "a"};
        List<String> tolist = Stream.of(testStrings).collect(Collectors.toList());
        Set<String> toset = Stream.of(testStrings).collect(Collectors.toSet());
        //tomap的两个坑：https://blog.csdn.net/TANK2017/article/details/128089717
        Map<Integer, String> tomap = list.stream().collect(
                Collectors.toMap(User::getId, User::getName)
        );
        System.out.println("-----------Stream转换list------------");
        System.out.println(tolist);
        System.out.println("-----------Stream转换set------------");
        System.out.println(toset);
        System.out.println("-----------Stream转换map------------");
        System.out.println(tomap);

        //自定义Collection的数据结构
        LinkedList<User> toLinkedList = list.stream().collect(Collectors.toCollection(LinkedList::new));
        System.out.println("-----------Stream转换LinkedList------------");
        System.out.println(toLinkedList);
//        TreeSet<User> toTreeSet = list.stream().collect(Collectors.toCollection(TreeSet::new));
//        System.out.println("-----------Stream转换TreeSet------------");
//        System.out.println(toTreeSet);
    }

    /**
     * 分组
     *
     * @param list
     */
    private void group(List<User> list) {
        //分组
        Map<String, List<User>> groupby = list.stream().collect(Collectors.groupingBy(User::getType));
        System.out.println("-----------分组------------");
        System.out.println(groupby);

        //分组个数
        Map<String, Long> size = list.stream().collect(Collectors.groupingBy(User::getType, Collectors.counting()));
        System.out.println("-----------分组个数------------");
        System.out.println(size);

        //多级分组
        Map<String, Map<String, List<User>>> groupBy = list.stream().collect(Collectors.groupingBy(User::getType, Collectors.groupingBy(User::getName)));
        System.out.println("-----------多级分组------------");
        System.out.println(groupBy);
    }
```