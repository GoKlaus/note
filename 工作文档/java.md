 

http://www.importnew.com/27604.html

 

 

拦截器(Interceptor)   过滤器   监听器

 

 

===========================================================================================Java工程师成神之路===========================================================================================

http://www.importnew.com/17389.html

 

https://www.cnblogs.com/jpfss/p/9034881.html

===========================================================================================自己搭的框架===========================================================================================

http://www.importnew.com/20215.html

 

===========================================================================================去投资银行面试会遇到的10个Java问题===========================================================================================

http://www.importnew.com/29199.html

http://www.importnew.com/27326.html

http://www.importnew.com/23792.html

 

https://www.sohu.com/a/238910929_100111562

 

http://www.importnew.com/22083.html

 

http://www.importnew.com/22056.html

 

http://www.importnew.com/21445.html

http://www.importnew.com/19538.html

http://www.importnew.com/17232.html

http://www.importnew.com/16247.html

===========================================================================================疑问===================================================================================

http://www.importnew.com/22178.html

http://www.importnew.com/22046.html

 

http://www.importnew.com/21396.html

http://www.importnew.com/19681.html

 

http://www.importnew.com/19434.html

http://www.importnew.com/19275.html

 

http://www.importnew.com/18983.html

===========================================================================================道路===================================================================================

https://my.oschina.net/u/3779583/blog/1862418

 

 

JDK 1.5 中引入并发包之后，并发工具和并发集合备受欢迎，比如 ThreadLocal、 BlockingQueue、Counting Semaphore 和 ConcurrentHashMap，与这些工具相关的面试题也越来越多。

 

Java 8 和 Java 9 也是这种情况。围绕 lambda 表达式、并行流（parallel streams）、新的 Fork/Join 线程池、CompletableFuture 的问题在 2018 年不断涌现，2019 年还将持续。今后你也应该对这些知识点有所准备。

 

===========================================================================================保护眼睛===================================================================================

 

 

win7 : 【桌面】→ 【右键】→ 【个性化】→ 【窗口颜色】→ 【高级外观设置】→ 项目选择【窗口】→ 【颜色1（L）】（记住要选L项）→ 【选择（其它）】将色调自己设定为：85。饱和度：123。亮度：205→添加到自定义颜色→在自定义颜色选定→确定

===================================================================================================eclipse背景色===================================================================================

在eclipse中 windows-perferences-geneal-text-editors

在Apperences color options中选择Background color,去掉SYSTEM DEFAULT的勾，自定义RGB：

R 199 G 237 B 204

 

白天晚上都调到亮度30-40（开始会不习惯 时间长一点就好）（晚上最好开灯）

对比度70-80

右键——属性——外观——高级——项目选择——窗口——，在“颜色1（L）”下拉框中选择（其它），将色调改为85，饱和度改为123，亮度改为205，然后，添加到自定义颜色，最后确定。。。

完成这些步骤后，你的电脑屏幕显示的所有文档不再是刺眼的白底黑字，而是非常柔和温馨的豆沙绿。。。

这可是眼科专家专业配置的哦，长时间使用可以有效缓解眼睛疲劳，从而保护眼睛。。。

===========================================================================================数据库操作=================================================================================================================

Oracle  建立表空间和表:

用Xshell登录虚拟机，执行如下命令进入sql环境

\> su - oracle

\> sqlplus / as sysdba   //系统管理员身份

/*第1步：创建临时表空间  */

create temporary tablespace vdmonitor_temp      

tempfile '/opt/oracle/data/oradata/esight/vdmonitor_temp.dbf'

size 50m  

autoextend on  

next 50m maxsize 20480m  

extent management local;  

 

/*第2步：创建数据表空间  */

create tablespace vdmonitor  

logging  

datafile '/opt/oracle/data/oradata/esight/vdmonitor.dbf'

size 50m  

autoextend on  

next 50m maxsize 20480m  

extent management local;  

 

/*第3步：创建用户并指定表空间  */

create user vdmonitor identified by Changeme_123 default tablespace vdmonitor temporary tablespace vdmonitor_temp;

 

/*第4步：给用户授予权限  */

grant connect,resource,dba to vdmonitor;

 

Drop user reportfile cascade;

 

\> su - oracle

\> sqlplus chang/Changeme_123

SQL>

 

 

ALTER TABLE SITEMGR.TBL_SITE_INFO DROP COLUMN STARTTIME

 

alter table SITEMGR.TBL_SITE_INFO add STARTTIME number(20);

 

在安装Oracle之前必须创建“oracle”用户、“oinstall”组和“dba”组，其中：

只有“oracle”用户可以安装、启动和关闭Oracle数据库。

只有“oinstall”组的用户可以安装Oracle软件。

只有“dba”组的用户可以管理数据库。

 

Linux挂载分区：   /opt里空间大小不变，实际的内容存储在/dev/xvde1 这个分区里

sudo mount /dev/xvde1 /opt

 

sudo umount /dev/xvde1

 

===========================================================================================页面模型=================================================================================================================

import java.util.ArrayList;

import java.util.List;

import org.apache.commons.collections.CollectionUtils;

 

public class PageModel<T>

{

​    /**

​     \* 该页起始索引

​     */

​    private int pageBegin;

​    

​    /**

​     \* 页数

​     */

​    private int page;

​    

​    /**

​     \* 每页显示个数

​     */

​    private int pageLength;

​    

​    /**

​     \* 记录总数

​     */

​    private long totalRecord;

​    

​    /**

​     \* 每页结果集

​     */

​    private List<T> resultList;

​    

​    /**

​     \* 无参构造方法

​     */

​    public PageModel()

​    {

​    }

​    

​    /**

​     \* PageModel

​     \* @param allList allList

​     \* @param page page

​     \* @param pageLength pageLength

​     */

​    public PageModel(List<T> allList, int page, int pageLength)

​    {

​        this.page = page;

​        this.pageLength = pageLength;

​        if (CollectionUtils.isNotEmpty(allList))

​        {

​            this.totalRecord = allList.size();

​        }

​        List<T> tempList = new ArrayList<T>();

​        if (page == 0)

​        {

​            page = 1;

​        }

​        for (int i = (page - 1) * pageLength; (i < page * pageLength) && (i < totalRecord); i++)

​        {

​            tempList.add(allList.get(i));

​        }

​        this.resultList = tempList;

=============================================================================================类与DB表对应，将类的属性转化为表的属性==============================================================================================================

public static boolean isEmpty(String str)

​    {

​        return str == null || str.length() == 0;

​    }

 

//如果当前数据库字段值为空，则赋值一个空String类型的值, null=>""

public static Object convertEmptyStrValue(final String strValue)

​    {

​        if (StringUtils.isEmpty(strValue))

​        {

​            return new JdbcType(DataType.STRING);

​        }

​        return strValue;

​    }

单组数据：    

protected Map<String, Object> addDataParam(ServiceSetModel object)

​    {

​        Map<String, Object> map = new HashMap<String, Object>();

​        map.put("pkid", object.getPkid());

​        map.put("serviceset_name", CommonUtil.convertEmptyStrValue(object.getServicesetName()));

​        map.put("old_serviceset_name", CommonUtil.convertEmptyStrValue(object.getOldName()));

​        map.put("serviceset_type", CommonUtil.convertEmptyStrValue(object.getServicesetType()));

​        

​        if (null == object.isPreDefined())

​        {

​            object.setPreDefined(false);

​            map.put("pre_defined", object.isPreDefined());

​        }

​        else

​        {

​            map.put("pre_defined", object.isPreDefined());

​        }

​        map.put("serviceset_desc", CommonUtil.convertEmptyStrValue(object.getServicesetDesc()));

​        return map;

​    }

多组数据：

protected List<Map<String, Object>> addDataParams(List<ServiceSetModel> objects)

​    {

​        List<Map<String, Object>> dataRows = new ArrayList<Map<String, Object>>();

​        Map<String, Object> dataRow;

​        for (final ServiceSetModel object : objects)

​        {

​            dataRow = this.addDataParam(object);

​            dataRows.add(dataRow);

​        }

​        return dataRows;

​    }    

==============================================================================================分页查询==============================================================================================================

 

​     \* 分页查询

​     \* @param condition 条件

​     \* @param pageBegin 第几页查询

​     \* @param pageLength 每页显示熟路

​     \* @param isGlobal 是否全局

​     \* @return PageModel 带分页数据的服务信息

​     \* @throws OMSException  异常

​    

​     分页前台：

​     function getPageData(start, pageSize, condition) {    //start：从第几页开始:3  pageSize：每页的条数:10  condition：结果显示的顺序

​          var startpage = 0 + (start - 1) * pageSize;  //开始查询时的条数:20

​          Ajax-------->后台：

​          page = serviceSetMgrSrv.queryPage(condition, startpage, pageSize, true);  从20开始查询10条数据

​          

​          

===================================================================================ORACLE分页查询SQL语法——最高效的分页==============================================================================================

1:无ORDER BY排序的写法。(效率最高):

SELECT *

  FROM (SELECT ROWNUM AS rowno, t.*

​         FROM emp t

​         WHERE hire_date BETWEEN TO_DATE ('20060501', 'yyyymmdd')

​                             AND TO_DATE ('20060731', 'yyyymmdd')

​           AND ROWNUM <= 20) table_alias

WHERE table_alias.rowno >= 10;

 

2:有ORDER BY排序的写法。(效率最高)

SELECT *

  FROM (SELECT tt.*, ROWNUM AS rowno

​          FROM (  SELECT t.*

​                    FROM emp t

​                   WHERE hire_date BETWEEN TO_DATE ('20060501', 'yyyymmdd')

​                                       AND TO_DATE ('20060731', 'yyyymmdd')

​                ORDER BY create_time DESC, emp_no) tt

​         WHERE ROWNUM <= 20) table_alias

WHERE table_alias.rowno >= 10;

垃圾但又似乎很常用的分页写法:

SELECT *

  FROM (SELECT ROWNUM AS rowno, t.*

​          FROM k_task t

​         WHERE flight_date BETWEEN TO_DATE ('20060501', 'yyyymmdd')

​                               AND TO_DATE ('20060731', 'yyyymmdd')) table_alias

WHERE table_alias.rowno <= 20 AND table_alias.rowno >= 10;

--TABLE_ALIAS.ROWNO  between 10 and 100;

原因：

这是由于CBO优化模式下，Oracle可以将外层的查询条件推到内层查询中，

以提高内层查询的执行效率。对于第一个查询语句，第二层的查询条件WHERE ROWNUM <= 40就可以被Oracle推入到内层查询中，

这样Oracle查询的结果一旦超过了ROWNUM限制条件，就终止查询将结果返回了。

而第二个查询语句，由于查询条件BETWEEN 21 AND 40是存在于查询的第三层，

而Oracle无法将第三层的查询条件推到最内层（即使推到最内层也没有意义，因为最内层查询不知道RN代表什么）。

因此，对于第二个查询语句，Oracle最内层返回给中间层的是所有满足条件的数据，而中间层返回给最外层的也是所有数据。

数据的过滤在最外层完成，显然这个效率要比第一个查询低得多。

 

分页查询格式：《高效》！！！！！！！！！！！！！！！！！！！！！！！！！！！！

SELECT *

  FROM (SELECT a.*, ROWNUM rn

​          FROM (SELECT *

​                  FROM table_name) a

​         WHERE ROWNUM <= 40)

WHERE rn >= 21

我感觉要是理解的话还是从里面向外面更好一些，先是从一个表中获得数据select * from table_name,

再给这个表付上rn的值并且将索取的行数确定为100行select a.*,rownum rn from (select * from table_name) a where rownum<=100，

之后再确定从哪一行开始select * from (select a.*,rownum rn from (selecct * from table_name) a where rownum<=100) where rn>=10

​    

==============================================================================================带泛型的Iterator遍历==============================================================================================================

 

​    private List<ServiceSetItemModel> updateObjectItems(List<ServiceSetModel> serviceSets, List<Long> pkids)

​    {

​        List<ServiceSetItemModel> list = new ArrayList<ServiceSetItemModel>();

​        for (Iterator<ServiceSetModel> iterator = serviceSets.iterator(); iterator.hasNext();)

​        {

​            ServiceSetModel serviceSet = iterator.next();

​            List<ServiceSetItemModel> temp = updateObjectItems(serviceSet, pkids);

​            list.addAll(temp);

​        }

​        return list;

​    }

​    

​    Iterator<Map.Entry<Integer,String>> it = m.entrySet().iterator();

​        while(it.hasNext()){

​            Map.Entry<Integer,String> entry = it.next();

​            int key = entry.getKey();

​            if(key == 2){

​                it.remove();

​            }

​        }

​    

 

==============================================================================================批量操作结果数据类型==============================================================================================================    

public class BatchOptResultModel

{

​    private static final String OPERATE_STATUS_SUCCESS = "enterprise.app.securecenter.operate.status.success";

 

​    /**

​     \* 当前操作的整体结果：成功，部分成功，失败

​     */

​    private String result;

​    

​    /**

​     \* 每一个对象的操作结果集合

​     */

​    private List<EntItemDO> entItemList = new ArrayList<EntItemDO>();

​    

​    /** <一句话功能简述>

​     \* 根据当前每一条任务的结果信息计算该操作的结果

​     \* @param itemList 操作结果

​     \* @see [类、类#方法、类#成员]

​     */

​    public void buildOptResult(final List<EntItemDO> itemList)

​    {

​        this.entItemList = itemList;

​        int sucCount = 0;

​        for (final EntItemDO item : this.entItemList)

​        {

​            if (MessageUtil.getMessage(OPERATE_STATUS_SUCCESS)

​                .equals(item.getItemValue()))

​            {

​                sucCount++;

​            }

​        }

​        

​        if (sucCount == 0)

​        {

​            this.result = SecureCenterConstant.FAIL;

​        }

​        else if ((sucCount != 0) && (sucCount != this.entItemList.size()))

​        {

​            this.result = SecureCenterConstant.PARTSUCCESS;

​        }

​        else if (sucCount == this.entItemList.size())

​        {

​            this.result = SecureCenterConstant.SUCCESS;

​        }

​        

​    }

​    

}

==============================================================================================获取系统时间==============================================================================================================    

​     /**

​     \* @param format 格式化

​     \* @return String 当前系统时间

​     */

​    public static String getSysTime(final String format)

​    {

​        final SimpleDateFormat df = new SimpleDateFormat(format);     // 给定模式

​        return df.format(new Date());                                 // public final String format(Date date)

​    }

​    

​    getSysTime("yyyy-MM-dd HH:mm:ss")

 

==============================================================================================时间格式转换==============================================================================================================

public class TestOne

{

​    public static void main(String[] args) {

​        //String------>Date------>long

​        String str="2016-09-21";

​        Date date=null;

​        try {

​        date=new SimpleDateFormat("yyyy-MM-dd").parse(str);

​        } catch (ParseException e) {

​        // TODO Auto-generated catch block

​        e.printStackTrace();

​        }

​        Timestamp ts=new Timestamp(System.currentTimeMillis());

​        System.out.println(System.currentTimeMillis());

​        System.out.println(date);

​        System.out.println(ts.getTime());

​        System.out.println(date.getTime());

​        

​        //long------>Date------>String

​        Date date1 = new Date(1474387200000l);

​        SimpleDateFormat f = new SimpleDateFormat("yyyy-MM-dd");

​        String a = f.format(date1);

​        

​        System.out.println(a);

 

​        }

 

}

结果：

1474684047105

Wed Sep 21 00:00:00 GMT+08:00 2016

1474684047105

1474387200000

2016-09-21

 

Calendar calendar = Calendar.getInstance();

SimpleDateFormat formatter = new SimpleDateFormat("yyyy-MM-dd hh:mm:ss");

String r = formatter.format(calendar.getTime());

System.out.println(r);

结果：

2016-10-08 04:49:37

 

final SimpleDateFormat df = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");

String r2 = df.format(new Date());

System.out.println(r2);

结果：

2016-10-08 16:51:36

 

 

==============================================================================================DB与Model转换==============================================================================================================    

 

从DB中查询数据 select得到 ResultSet类型，但规范是返回集合

在ServiceSetModel类中定义的静态的方法

public static ServiceSetModel convertDBData2Object(final DataSet ds)

​    {

​        ServiceSetModel serviceSet = new ServiceSetModel();

​        serviceSet.setPkid(ds.getLong(DBCons.PKID));

​        serviceSet.setServicesetName(ds.getString(DBCons.SERVICE_SET_NAME));

​        serviceSet.setServicesetNameCn(ds.getString("serviceset_name_cn"));

​        serviceSet.setOldName(ds.getString("old_serviceset_name"));

​        serviceSet.setServicesetType(ds.getString("serviceset_type"));

​        serviceSet.setPreDefined(ds.getBoolean("pre_defined"));

​        serviceSet.setServicesetDesc(ds.getString("serviceset_desc"));

​        String details = ds.getString("details");

​        if (details == null || details.isEmpty())

​        {

​            serviceSet.setDetails(new String[0]);

​        }

​        else

​        {

​            serviceSet.setDetails(details.split("\n"));    //StringTokenizer

​        }

​        serviceSet.setLocked(ds.getBoolean(DBCons.LOCKED));

​        serviceSet.setLockedBy(ds.getString(DBCons.LOCKED_BY));

​        serviceSet.setUniqueCode(ds.getLong(DBCons.UNIQUE_CODE));

​        serviceSet.setAdomName(ds.getString(DBCons.ADOM_NAME));

​        serviceSet.setDeviceDn(ds.getString(DBCons.DEVICE_DN));

​        

​        return serviceSet;

​    }

​    

​    protected void addResult(DataSet dataSet, List<ServiceSetModel> list)

​    {

​        ServiceSetModel object = ServiceSetModel.convertDBData2Object(dataSet);

​        

​        list.add(object);

​        

​    }

​    

​    protected List<ServiceSetModel> addResult(DataSet dataSet)

​    {

​        List<ServiceSetModel> list = new ArrayList<ServiceSetModel>();

​        if (null == dataSet)

​        {

​            return list;

​        }

​        while (dataSet.next())

​        {

​            addResult(dataSet, list);

​        }

​        return list;

​    }

​    

​    

​    DataSet ds = DBPersistenceService.query(DBCons.TBL_GLOBAL_RES_SERVICESET, columnNames, criterion);

​    List<ServiceSetModel> resultList = new List<ServiceSetModel>();

​    resultList.addAll(addResult(ds));

​    

 

 

 

==============================================================================================DB主键自增==============================================================================================================    

public class AtomicLong extends Number implements java.io.Serializable {   //API中的类 ，亦可以是 AtomicInteger

   private volatile long value;

   public AtomicLong(long initialValue) {

​       value = initialValue;

   }

   public AtomicLong() {

   }

   public final long get() {

​       return value;

   }

   public final long incrementAndGet() {

​        for (;;) {

​            long current = get();

​            long next = current + 1;

​            return next;

​        }

   }

}

 

public abstract class PkidGenerator

{

​    private static AtomicLong startIndex = new AtomicLong(System.currentTimeMillis());

​    

​    public static long getGenerateId()

​    {

​        return startIndex.incrementAndGet();

​    }

}

 

// main()方法中：   PkidGenerator.getGenerateId();

 

==================================================================================================基础类==============================================================================================================    

 

\* 基础类

public class BaseObject implements Cloneable, Serializable

{

​    /**

​     \* serialVersionUID

​     */

​    private static final long serialVersionUID = -167880734944180921L;

​    /**

​     \* {@inheritDoc}

​     */

​    @Override

​    protected BaseObject clone() // NOPMD by t00201981

​    {

​        try

​        {

​            return (BaseObject)super.clone();

​        }

​        catch (CloneNotSupportedException e)

​        {

​            throw new Error(e); // NOPMD by t00201981

​        }

​    }

}

 

基础业务模型：

public class BusinessObject extends BaseObject{

​    protected long bakid;

​    protected String deviceDn;

​    protected String name;

​         。

​         。        

​         。

​         。        

}

 

具体的业务对象：  ServiceSetModel

public class ServiceSetModel extends BusinessObject{

​    /**

​     \* serialVersionUID

​     */

​    private static final long serialVersionUID = 927765420268011351L;

​    

​    private String servicesetName;

​    private String servicesetType;

​         。

​         。        

​         。

​         。        

​    @Override

​    public void setPkid(final long pkid)

​    {

​        super.setPkid(pkid);

​        

​        for (final ServiceSetRelGroupModel item : rels)    //在Model中实现主键约束

​        {

​            item.setServicesetId(pkid);

​        }

​    }    

 

​    @Override

​    /**

​     \* 将对象内容转换成按属性Map

​     \* @return Map

​     */

​    public Map<String, Object> toContentMap()

​    {

​        final Map<String, Object> contentMap = new LinkedHashMap<String, Object>();

​        contentMap.put("description", servicesetDesc == null ? "" : servicesetDesc);

​        contentMap.put("serviceset type", servicesetType);

​        

​        List<String> memberContents = new ArrayList<String>();

​        for (final ServiceSetItemModel item : items)

​        {

​            final String memberContent = item.toContentString();

​            memberContents.add(memberContent);

​        }

​        contentMap.put("member", memberContents);

​        

​        List<String> itemContents = new ArrayList<String>();

​        

​        for (final ServiceSetRelGroupModel rel : rels)

​        {

​            itemContents.add(rel.getSubservicesetName());

​        }

​        

​        contentMap.put("reference service", itemContents);

​        appendContentMap(contentMap);

​        return contentMap;

​    }

 

​     /**

​     \* 根据后台数据转换相应的服务信息

​     *

​     \* @param ds 后台数据库数据

​     \* @return List<ServiceSetModel> 服务列表

​     */

​    public static List<ServiceSetModel> convertDBData2ServiceList(final DataSet ds)

​    {

​        final List<ServiceSetModel> result = new LinkedList<ServiceSetModel>();

​        final List<String> nameList = new ArrayList<String>();

​        nameList.addAll(CommonUtil.convertStrValue2List(ds.getString(DBCons.SERVICE_SET_NAME)));     //serviceset_name

​        nameList.addAll(CommonUtil.convertStrValue2List(ds.getString(DBCons.SERVICE_GROUP_SET_NAME)));

​        final List<String> idList = new ArrayList<String>();

​        idList.addAll(CommonUtil.convertStrValue2List(ds.getString(DBCons.SERVICE_SET_ID)));

​        idList.addAll(CommonUtil.convertStrValue2List(ds.getString(DBCons.SERVICE_GROUP_SET_ID)));

​        

​        for (int index = 0; index < nameList.size(); index++)

​        {

​            final ServiceSetModel newService = new ServiceSetModel();

​            newService.setPkid(Long.parseLong(idList.get(index)));

​            newService.setServicesetName(nameList.get(index));

​            result.add(newService);

​        }

​        

​        return result;

​    }

​    

​    单行数据：

​    public static ServiceSetModel convertDBData2Object(final DataSet ds)

​    {

​        ServiceSetModel serviceSet = new ServiceSetModel();

​        serviceSet.setPkid(ds.getLong(DBCons.PKID));

​        serviceSet.setServicesetName(ds.getString(DBCons.SERVICE_SET_NAME));

​        serviceSet.setServicesetNameCn(ds.getString("serviceset_name_cn"));

​        serviceSet.setOldName(ds.getString("old_serviceset_name"));

​        serviceSet.setServicesetType(ds.getString("serviceset_type"));

​        serviceSet.setPreDefined(ds.getBoolean("pre_defined"));

​        serviceSet.setServicesetDesc(ds.getString("serviceset_desc"));

​        serviceSet.setLocked(ds.getBoolean(DBCons.LOCKED));

​        serviceSet.setLockedBy(ds.getString(DBCons.LOCKED_BY));

​        serviceSet.setUniqueCode(ds.getLong(DBCons.UNIQUE_CODE));

​        serviceSet.setDeviceDn(ds.getString(DBCons.DEVICE_DN));

​        

​        return serviceSet;

​    }

​    

​    //ToMap

​    public static Map<Long, ServiceSetModel> convertDBData2VOMap(final DataSet ds)

​    {

​        HashMap<Long, ServiceSetModel> map = new HashMap<Long, ServiceSetModel>();

​        ServiceSetModel serviceSetModel;

​        Long pkid;

​        while (ds.next())

​        {

​            pkid = ds.getLong(DBCons.PKID);

​            serviceSetModel = map.get(pkid);                                    //重要

​            if (serviceSetModel == null)

​            {

​                serviceSetModel = convertDBData2Object(ds);

​            }

​            map.put(pkid, serviceSetModel);

​            

​            addItemsToVo(serviceSetModel, ds);   //serviceSetItemModel

​            addRelsToVo(serviceSetModel, ds);    //serviceSetRelGroupModel

​        }

​        return map;

​    }

 

​    

​        

}

 

==================================================================================================层次。。接口继承另一个接口==============================================================================================================    

 

 

 

 

 

=====================================================================================================持久层《抽象类》  持久层Dao类必须是单例============================================================================================    

 

public abstract class ServiceSetDao

{

​    private static final OMSLog LOGGER = OMSLogFactory.getLog(ServiceSetDao.class);

​    

​    private static final String tblName = SiteMgrConstants.TABLE_SITEMGR;

​    

​    private static final String preName = SiteMgrConstants.NAMINGSQL_TABLE_SITEMGR_PREFIX;

​        

​    //单例

​    private static ServiceSetDao INSTANCE = null;

 

​    public static ServiceSetDao getInstance()

​    {

​        if (null == INSTANCE)

​        {

​            INSTANCE = new ServiceSetDao();

​        }

​        return INSTANCE;

​    }

​                              |

​                              |

​                             \|/

 

​    private static final GlobalServiceSetItemDao INSTANCE = new GlobalServiceSetItemDao();

​    public static GlobalServiceSetItemDao getInstance()

​    {

​        return INSTANCE;

​    }

​    

​    public void add(final ServiceSetModel object)                                                //持久层的方法参数是 业务层类型的对象

​        throws OMSException

​    {

​        final List<Map<String, Object>> dataRows = new ArrayList<Map<String, Object>>();

​        dataRows.add(addDataParam(object));   ！！！！！！！！！！！！！！！！！！！！！！！！！ //持久层的方法参数是 业务层类型的对象,所以将 业务层类型的对象映射成 更一般类型的对象。然后由进一步封装后更一般的类调用

​        DBPersistenceService.insert(tblName, dataRows);                                          //DBPersistenceService：数据库操作封装,不再操作业务层类型的对象,而是操作更一般的对象，此一般对象 采用Map<String, Object>

​                                                                                                                         类型，String一定为数据库字段，Object为与之对应业务层类型的对象的值

​    }

​                              |

​                              |

​                             \|/    

​    //将服务对象属性和数据库字段对应

​    protected Map<String, Object> addDataParam(ServiceSetModel object)

​    {

​        Map<String, Object> map = new HashMap<String, Object>();

​        map.put("pkid", object.getPkid());

​        map.put("serviceset_name", CommonUtil.convertEmptyStrValue(object.getServicesetName()));   //表中不能塞null

​        map.put("old_serviceset_name", CommonUtil.convertEmptyStrValue(object.getOldName()));

​        map.put("serviceset_type", CommonUtil.convertEmptyStrValue(object.getServicesetType()));

​        

​        if (null == object.isPreDefined())

​        {

​            object.setPreDefined(false);

​            map.put("pre_defined", object.isPreDefined());

​        }

​        else

​        {

​            map.put("pre_defined", object.isPreDefined());

​        }

​        map.put("serviceset_desc", CommonUtil.convertEmptyStrValue(object.getServicesetDesc()));

​        return map;

​    }

}

 

=====================================================================================================业务层《接口》============================================================================================    

 

public interface IBusinessService<T extends BusinessObject>{                                        //公共的增删改查

​    void addBatch(List<T> objects, boolean isGlobal) throws OMSException;

​    void updateBatch(List<T> objects, boolean isGlobal) throws OMSException;

​    void deleteBatch(List<Long> pkids, boolean isGlobal) throws OMSException;

​    List<T> query(Map<String, Object> condition, boolean isGlobal) throws OMSException;

}

 

public interface IServiceSetMgrSrv extends IBusinessService<ServiceSetModel>{                      //自己特有的方法

​    public boolean validateIsExist(String name, boolean isGlobal) throws OMSException;

​    PageModel<ServiceSetModel> queryPage(Map<String, Object> condition, int pageBegin, int pageLength,final boolean isGlobal)throws OMSException;

​    List<ServiceSetModel> viewBypkIds(Collection<Long> pkids, final boolean isGlobal) throws OMSException;

​    List<ServiceSetModel> queryUnusedByPkids(final String pkids)throws OMSException;

}

 

业务层中注入持久层

final List<ServiceSetModel> sets =

​     ServiceSetDao.getInstance(isGlobal).queryPage(conditionSet, pageBegin, pageLength);          //持久层的方法参数是 表现层类型的对象

 

 

====================================================================================================请求处理层=============================================================================================    

 

表现层的每一个单独的服务内 单独引入业务层实例，这是因为不知道先调那个服务

public class ApplicationROAService

{

​    

​    private static final OMSLog LOGGER = OMSLogFactory.getLog(ApplicationROAService.class);

​    

​    IApplicationMgrSvc applicationSetService;   //接口定义类

​    

​    //添加应用日志

​    public void operLog(final List<OperLogResult> operLogResultListSuc, final String operation,

​    final LogResult operresult, final String operationDetail)

​    {

​        

​        OperLogUtils.getInstance().writeOperLog(operationDetail,

​            operation,

​            LogSeverity.MINOR,

​            operresult,

​            operLogResultListSuc);

​    }

​    

​    @PUT

​    @Path("viewData")

​    public final PageModel<ApplicationModel> queryData(@QueryParam("condition")

​    final String condition, @QueryParam("start")

​    final int start, @QueryParam("pageSize")

​    final int pageSize)

​        throws ServiceException, OMSException

​    {

​        if (null == applicationSetService)     //非常重要 如果有只调一次

​        {

​            getapplicationSetService();

​        }

​               .

​               .               

​               .    

​               .

​    }

​    

​    @PUT

​    @Path("queryUnionData")

​    public final PageModel<ApplicationModel> queryUnionData(@QueryParam("condition")

​    final String condition, @QueryParam("start")

​    final int start, @QueryParam("pageSize")

​    final int pageSize)

​        throws ServiceException, OMSException

​    {

​        if (null == applicationSetService)

​        {

​            getapplicationSetService();

​        }

​               .

​               .               

​               .    

​               .

​    }

​    

​     /**

​     \* getapplicationSetService

​     */

​    private void getapplicationSetService()

​    {

​        applicationSetService = ServiceFactory.getInstance().getService(IApplicationMgrSvc.class);

​    }

}

 

==================================================================================================将Json对象转换成Map============================================================================================

public static Map<String, String> toMap(final String jsonString)

​    {

​        final Map<String, String> result = new HashMap<String, String>();

​        JSONObject jsonObject = null;

​        try

​        {

​            jsonObject = new JSONObject(jsonString);                   //法2：JSONObject jso = JSONObject.fromObject(Object object);

​        }

​        catch (final JSONException e)

​        {

​            LOGUPGRADEMGR.error("JsonHelper##toMap new jsonobject parse json error.");

​        }

​        if (null == jsonObject)

​        {

​            return result;

​        }

​        

​        final Iterator iterator = jsonObject.keys();

​        String key = null;

​        String value = null;

​        

​        while (iterator.hasNext())

​        {

​            

​            key = (String)iterator.next();

​            try

​            {

​                value = jsonObject.getString(key);

​            }

​            catch (final JSONException e)

​            {

​                LOGUPGRADEMGR.error("JsonHelper##toMap jsonobject getstring parse json error.");

​            }

​            result.put(key, value);

​            

​        }

​        return result;

​    }

​    

​    

（1）Hint概念

http://dbaplus.cn/news-10-669-1.html

（2）Hint例子

http://hbxztc.blog.51cto.com/1587495/1908309

（3）索引学习

[https://books.google.com/books?id=5MuxS6tbPb4C&pg=PA235&lpg=PA235&dq=Oracle+%E7%B4%A2%E5%BC%95%E5%85%A5%E9%97%A8&source=bl&ots=5TlORHTPIi&sig=hTKn67P9KMpQu1KAA6qNc0B1Iys&hl=zh-CN&sa=X&ved=0ahUKEwid27qaz7PXAhUj44MKHbfJBWIQ6AEIJjAA#v=onepage&q=Oracle%20%E7%B4%A2%E5%BC%95%E5%85%A5%E9%97%A8&f=false](https://books.google.com/books?id=5MuxS6tbPb4C&pg=PA235&lpg=PA235&dq=Oracle+索引入门&source=bl&ots=5TlORHTPIi&sig=hTKn67P9KMpQu1KAA6qNc0B1Iys&hl=zh-CN&sa=X&ved=0ahUKEwid27qaz7PXAhUj44MKHbfJBWIQ6AEIJjAA#v=onepage&q=Oracle 索引入门&f=false)

（4）优化方式

http://oxiaobai.blog.51cto.com/3369332/752142

（5）执行计划含义

http://blog.csdn.net/u013933870/article/details/51730130

%CPU含义

http://t.askmaclean.com/thread-4780-1-1.html

（6）全表扫描

http://blog.csdn.net/leshami/article/details/8971930

 

 

 

我:

==================================================================================================将String转换成List============================================================================================    

​        public static List<String> transformJsonToList(final String jsonData)

​    {

​        final List<String> dataList = new ArrayList<String>();

​        if ((null == jsonData) || jsonData.isEmpty())

​        {

​            return dataList;

​        }

​        String[] list = null;

​        list = jsonData.split(",");       //StringTokenizer

​        for (final String string : list)

​        {

​            dataList.add(string);

​        }

​        

​        return dataList;

​    }

==================================================================================================Java中操作节点==================================================================================================

 

Document doc

Element root = doc.getDocumentElement();  //根节点

final Node node = root.getElementsByTagName(dbType).item(0);  //getElementsByTagName返回NodeList类型

final NodeList nodeList = node.getChildNodes();

Node childNode = nodeList.item(i);

final String item = childNode.getTextContent().trim();

我:

======================================================================================字符串操作  从字符串A中 找出字符串B 将其替换成字符串C===========================================================

从字符串A中 找出字符串B 将其替换成字符串C

String是不可变类

public class StringUtils

{

​    public static String replace(String text, String searchString, String replacement, int max)

​    {

​        int start = 0;

​        int end = text.indexOf(searchString, start);

​        if (end == -1)

​        {

​            return text;

​        }

​        int replLength = searchString.length();

​        int increase = replacement.length() - replLength;

​        increase = (increase < 0) ? 0 : increase;

​        increase *= ((max > 64) ? 64 : (max < 0) ? 16 : max);

​        StringBuffer buf = new StringBuffer(text.length() + increase);

​        while (end != -1)

​        {

​            buf.append(text.substring(start, end)).append(replacement);

​            start = end + replLength;

​            if (--max == 0)

​            {

​                break;

​            }

​            end = text.indexOf(searchString, start);

​        }

​        buf.append(text.substring(start));

​        return buf.toString();

​    }

​    

​    public static void main(String[] args)

​    {

​        String text = "123456789056789";

​        String searchString = "56789";

​        String replacement = "abcdefg";

​        String res = replace(text, searchString, replacement, -1);

​        System.out.println(res);   //1234abcdefg0abcdefg

​    }

}

​                   |

​                   |

​                   |

​                  \|/

可以用来进行 oracle转义符escape转换，需要转义的字符：_ % \

String [] a = {"_","%","\"};

String strConvert = "\";

List<String> eacapeList = Arrays.asList(a);

for (final String escapeChar : eacapeList)

{

​    clauseValue = StringUtils.replace(clauseValue, escapeChar, strConvert + escapeChar);

}

 

同理：  如要将String直接传到SQL中执行，字符串中’的要转换成2个’

例：  where a like 'haa

我:

======================================================================================字符串操作  从字符串A中 找出字符串B 返回下标===========================================================

 

1.从ordinal下标开始第一次找到字符串B时的下标

​    public static int ordinalIndexOf(String str, String searchStr, int ordinal)

​    {

​        if ((str == null) || (searchStr == null) || (ordinal <= 0))

​        {

​            return -1;

​        }

​        if (searchStr.length() == 0)

​        {

​            return 0;

​        }

​        int found = 0;

​        int index = -1;

​        while (index < ordinal)

​        {

​            index = str.indexOf(searchStr, index + 1);    //！！！！！！！！！！！！！！！！！！！！！重要

​            if (index < 0)

​            {

​                return index;

​            }

​        } ;

​        return index;

​    }

​    

2.从找到字符串B时的最后一次的下标

有现成的方法      str.lastIndexOf(searchChar);   

​                  str.lastIndexOf(searchChar, startPos);

​                  str.lastIndexOf(searchStr);

​                  str.lastIndexOf(searchStr, startPos);

 

 

==================================================================================================StringUtil============================================================================================        

​    

​    public static String trim(String str)

​    {

​        return ((str == null) ? null : str.trim());

​    }

​    

============================    

​    public static boolean equals(String str1, String str2)

​    {

​        return ((str1 == null) ? false : (str2 == null) ? true : str1.equals(str2));

​    }

============================    

​    

​    String a = "abc0efghijklmf";

​    int i4 = a.indexOf("f", 2);

​    System.out.println(i4);

​    

​    String a = "abc0efghijklmf";

​    int i4 = a.indexOf("fgh", 2);

​    System.out.println(i4);  //5

============================    

​    

​    public static boolean contains(String str, String searchStr)

​    {

​        if ((str == null) || (searchStr == null))

​        {

​            return false;

​        }

​        return (str.indexOf(searchStr) >= 0);

​    }

============================    

​    char ch = str.charAt(i);

============================

​    char[] searchChars = searchStr.toCharArray()

​    

============================

​    public String substring(int beginIndex) {

​        if (beginIndex < 0) {

​            throw new StringIndexOutOfBoundsException(beginIndex);

​        }

​        int subLen = value.length - beginIndex;

​        if (subLen < 0) {

​            throw new StringIndexOutOfBoundsException(subLen);

​        }

​        return (beginIndex == 0) ? this : new String(value, beginIndex, subLen);

​    }

 

​    public String substring(int beginIndex, int endIndex) {

​        if (beginIndex < 0) {

​            throw new StringIndexOutOfBoundsException(beginIndex);

​        }

​        if (endIndex > value.length) {

​            throw new StringIndexOutOfBoundsException(endIndex);

​        }

​        int subLen = endIndex - beginIndex;

​        if (subLen < 0) {

​            throw new StringIndexOutOfBoundsException(subLen);

​        }

​        return ((beginIndex == 0) && (endIndex == value.length)) ? this

​                : new String(value, beginIndex, subLen);

​    }

我:

==================================================================================================JSONArray解析================================================================================================

​        String jsonArrayString = "[{'sdn':'1475121224155','siteName':'sss'},{'sdn':'1475114924358','siteName':'南京1'}]";

​        final JSONArray jsonArray = new JSONArray(jsonArrayString);

​        JSONObject object = null;

​        Map<String,String> map = new HashMap<String,String>();

​        for (int i = 0; i < jsonArray.length(); i++)

​        {

​            object = jsonArray.getJSONObject(i);

​            map.put(object.getString("sdn"), object.getString("siteName"));

​        }

​        System.out.println("chang"+map.toString());

​        

​        chang{1475114924358=南京1, 1475121224155=sss}

我:

=================================================================================================排序问题================================================================================================

 

int a[] = {4,32,45,32,65,32,2} ;

Arrays.sort(a);     数组排序后的顺序:2 4 32 32 32 45 65

 

String[] str = { "a", "e", "f", "g", "h", "i", "b", "c", "d" };

Arrays.sort(str);  

Arrays.toString(str)；    ====>[a, b, c, d, e, f, g, h, i]

 

Arrays.sort(str, Collections.reverseOrder());

Arrays.toString(str)；    ====>[i, h, g, f, e, d, c, b, a]

 

 

 

法2：SiteModel实现Comparable接口：

​    @Override

​    public int compareTo(final Object o)

​    {

​        final SiteModel othSiteModel = (SiteModel)o;

​        final int othRemainingTime = Integer.parseInt(othSiteModel.getTimeRemaining());

​        final int thisRemainingTime = Integer.parseInt(this.timeRemaining);

​        return thisRemainingTime - othRemainingTime;

​    }

​    

​    

final List<SiteModel> siteModels = new ArrayList<SiteModel>();    

Collections.sort(siteModels);

 

 

法2：Book未实现Comparable接口，自定义比较器

public class Book  {

​    private int id;

​    private String name;

​    private double price;

​    private GregorianCalendar calendar;

}

 

 

Book b1 = new Book(1,"红楼",106.11,new GregorianCalendar(2009,01,01));

Book b2 = new Book(2,"西游",101.11,new GregorianCalendar(2008,01,01));

Book b3 = new Book(3,"水浒",102.11,new GregorianCalendar(2007,01,01));

List<Book> Booklist = new ArrayList<Book>();

Booklist.add(b1);

Booklist.add(b2);

Booklist.add(b3);

 

//自定义比较器实现Comparator接口

public class PriceComparator implements Comparator{

​    @Override

​    public int compare(Object o1, Object o2) {

​        Book bk1 = (Book)o1;

​        Book bk2 = (Book)o2;

​        return new Double(bk1.getPrice()).compareTo(new Double(bk2.getPrice()));    //    public int compareTo(Double anotherDouble) { return Double.compare(value, anotherDouble.value);}   Double.classd 的方法

​    }

}

 

 

则：

Collections.sort(Booklist, new PriceComparator());   自定义排序

 

 

================================================================================hashCode、equals====================================================================================================================

法3：判断对象是否相等

Book.java中：

​    public boolean equals(Object obj) {

​        if (this == obj)

​            return true;

​        if (obj == null)

​            return false;

​        if (getClass() != obj.getClass())

​            return false;

​        Book other = (Book) obj;

​        return new EqualsBuilder().append(this.id,other.id)

​                                  .append(this.name,other.name)

​                                  .append(this.price,other.price)

​                                  .isEquals();

​    }

 

Book b1 = new Book(1,"红楼",106.11,new GregorianCalendar(2009,01,01));

Book b2 = new Book(1,"红楼",106.11,new GregorianCalendar(2001,01,01));

Book b3 = new Book(1,"红楼",107.11,new GregorianCalendar(2009,01,01));

b1.equals(b2)  ===>true

b1.equals(b3)  ===>false

 

 

补充：自动生成HashCode： HashCodeBuilder(int  int)

​    public int hashCode() {

​        return new HashCodeBuilder(17,37).append(this.id)

​                                         .append(this.name)

​                                         .hashCode();

​    }

 

EqualsBuilder用在Equals()中   HashCodeBuilder用在hashCode()中

我:

==================================================================================================上传文件校验================================================================================================

 

 

public static int flieUploadCheck(final String path)

​    

​    {

​        if (null != path)

​        {

​            //文件路径长度大于2K

​            if (path.length() > 2000)

​            {

​                return 1;

​            }

​            final File file = new File(path);

​            final String fileName = file.getName();

​            final String type =

​                fileName.substring((fileName.length() - fileName.lastIndexOf(".")) - 1, fileName.length());

​            //黑名单方式，不支持exe , bat格式文件

​            if (type.equals("exe") || type.equals("bat"))

​            {

​                return 2;

​            }

​            //文件大小不大于20M

​            if (file.length() > (20 * 1024 * 1024))

​            {

​                return 3;

​            }

​            return MaintenancereportConstants.REQUEST_SUCCESS;

​        }

​        else

​        {

​            return MaintenancereportConstants.REQUEST_ERROR;

​        }

​    }

​    

 

​    

public static Map<String, Object> upload(final HttpServletRequest req, final String path)

​    {

​        int result = MaintenancereportConstants.REQUEST_SUCCESS;

​        final Map<String, Object> formMap = new HashMap<String, Object>();

​        // 未解析类提供配置信息

​        final DiskFileItemFactory factory = new DiskFileItemFactory();

​        // 创建解析类的实例

​        final ServletFileUpload sfu = new ServletFileUpload(factory);

​        final ServletRequestContext src = new ServletRequestContext(req);

​        // 每个表单域中的数据会封装到一个对应的FileItem对象上

​        List<FileItem> items = null;

​        //用于存放文件对象

​        FileItem uploadFileItem = null;

​        // 定义文件名

​        String fileName = "";

​        try

​        {

​            items = sfu.parseRequest(src);

​            for (final FileItem item : items)

​            {

​                // 判断是否是普通类型的表单,如果不是那么就是file类型

​                if (!item.isFormField())

​                {

​                    // 得到文件名

​                    fileName = item.getName();

​                    if (fileName.isEmpty())

​                    {

​                        continue;

​                    }

​                    else

​                    {

​                        formMap.put(MaintenancereportConstants.REPORT_NAME, fileName);

​                        uploadFileItem = item;

​                    }

​                }

​                else

​                {

​                    //把除文件外其他内容放入map中作为返回值传回

​                    formMap.put(item.getFieldName(), new String(item.getString().getBytes("iso8859-1"), "utf-8"));

​                }

​            }

​        }

​        catch (final FileUploadException e)

​        {

​            LOG.debug("写文件失败", e);

​            result = MaintenancereportConstants.REQUEST_ERROR;

​            formMap.put("result", result);

​        }

​        catch (final UnsupportedEncodingException e)

​        {

​            LOG.debug("转码出错", e);

​            result = MaintenancereportConstants.REQUEST_ERROR;

​            formMap.put("result", result);

​        }

​        //判断是否存在路径，若不存在，新建

​        final File folder = new File(path + File.separator + formMap.get(MaintenancereportConstants.REPORT_SDN));

​        if (!folder.exists() && !folder.isDirectory())

​        {

​            LOG.info("新建节点文件夹");

​            folder.mkdirs();

​        }

​        // 写入文件

​        final File file = new File(folder.getPath() + File.separator + fileName);

​        try

​        {

​            uploadFileItem.write(file);

​        }

​        catch (final Exception e)

​        {

​            LOG.debug("写文件失败", e);

​            result = MaintenancereportConstants.REQUEST_ERROR;

​            formMap.put("result", result);

​        }

​        return formMap;

​    }

 

​    

​    /**

​     \* 文件下载

​     \* <功能详细描述>

​     \* @param request request请求

​     \* @param response HttpServletResponse

​     \* @param path 文件路径

​     \* @see [类、类#方法、类#成员]

​     */

​    public static void download(final HttpServletRequest request, final HttpServletResponse response, final String path)

​    {

​        InputStream fis = null;

​        OutputStream toClient = null;

​        try

​        {

​            // path是指欲下载的文件的路径。

​            final File file = new File(path);

​            // 取得文件名。

​            String filename = file.getName();

​            // 以流的形式下载文件。

​            fis = new BufferedInputStream(new FileInputStream(path));

​            final byte[] buffer = new byte[fis.available()];

​            fis.read(buffer);

​            fis.close();

​            // 清空response

​            response.reset();

​            

​            // 现在中文文件名乱码问题

​            // 针对IE或IE内核的浏览器

​            if (request.getHeader("User-Agent").toUpperCase().indexOf("MSIE") > 0)

​            {

​                filename = URLEncoder.encode(filename, "UTF-8");

​            }

​            // 非IE浏览器的处理

​            else

​            {

​                filename = new String(filename.getBytes("UTF-8"), "ISO8859-1");

​            }

​            response.setContentType("application/x-download;charset=utf-8");

​            response.addHeader("Content-Disposition", String.format("attachment;filename=\"%s\"", filename));

​            response.setCharacterEncoding("UTF-8");

​            toClient = new BufferedOutputStream(response.getOutputStream());

​            toClient.write(buffer);

​            toClient.flush();

​            toClient.close();

​        }

​        catch (final IOException ex)

​        {

​            LOG.error("download is failed");

​        }

​        finally

​        {

​            try

​            {

​                if (null != fis)

​                {

​                    fis.close();

​                }

​            }

​            catch (final IOException e)

​            {

​                LOG.error("download is failed");

​            }

​            

​            try

​            {

​                if (null != toClient)

​                {

​                    toClient.close();

​                }

​            }

​            catch (final IOException e)

​            {

​                LOG.error("download is failed");

​            }

​        }

​    }

​    

​    

​    

​    /**

​     \* 删除指定该局点保存的所有文件

​     \* <功能详细描述>

​     \* @param file 需要删除的文件夹

​     \* @see [类、类#方法、类#成员]

​     */

​    public static void clearDir(final File file)

​    {

​        if (file.isDirectory())

​        {

​            for (final File f : file.listFiles())

​            {

​                //递归函数

​                clearDir(f);

​                f.delete();

​            }

​        }

​        file.delete();

​    }

​    

我:

=================================================================================================web.xml中配置Servlet================================================================================================

 

 

​    <servlet>

​        <description></description>

​        <display-name>HttpUploadServlet</display-name>

​        <servlet-name>HttpUploadServlet</servlet-name>

​        <servlet-class>enterprise.app.maintenancereport.ui.servlet.HttpUploadServlet</servlet-class>

​    </servlet>

​    <servlet-mapping>

​        <servlet-name>HttpUploadServlet</servlet-name>

​        <url-pattern>/v1/report/upReportFile</url-pattern>

​    </servlet-mapping>

 

==================================================================================================编码规范之最小化推进===============================================================================================

一：if仅用来判断错误的情形

if(true){

....

}else{

....

}

这种方式不合理，应该改成

if(error){

....

}

success code

 

二：if不要出先嵌套

if(A){...}

else {if(B){...}}

这种方式不合理，应该改成

if(A){...  return;}

if(B){...  return;}

 

 

=======================================================================================================编码规范===============================================================================================

 

Map<String,Object> m = new HashMap<String,Object>();

m = xxutil.getMap();

 

局部变量map下面已经赋值了，上面为啥初始化，没有任何意义

 

 

用三目运算符代替if  else

((uploadtime == null) ? 0 : uploadtime.hashCode())

 

 

 

 

=======================================================================================================枚举===============================================================================================

public enum Result {

​    SUCCESSFUL, FAILURE, POK;

 

​    private int intValue;

 

​    public int getIntValue() {

​        return ((this.intValue == 0) ? 0 : this.intValue);

​    }

 

​    public static Result getResult(int intValue) {

​        return values()[intValue];

​    }

}

 

Result boolresult = Result.SUCCESSFUL;

我:

==============================================================================================ROA创建服务层实例  单例===============================================================================================

Controller层调用服务层的服务，注入服务层的对象：

public class SiteMgrROAServiceImpl implements ISiteService

​    private static ISiteMgr siteMgr = null;

​    

​    public static void setSiteMgr(final ISiteMgr siteMgrIntf)

​    {

​        siteMgr = siteMgrIntf;

​    }

}

 

​    service.xml:

​    <bean name="ServiceHandler" factory-method="getInstance"  class="[enterprise.app.sitemgr.as.common.ServiceHandler](http://enterprise.app.sitemgr.as.common.servicehandler/)">

​        <property name="siteMgr" ref="siteMgrImpl"/>

​    </bean>

​    

​    <bean name="siteMgrImpl" class="enterprise.app.sitemgr.as.site.SiteMgr" />

 

​    

​    

​    

public class ServiceHandler

{

​    private static ServiceHandler instance = null;

​    

​    private ISiteMgr siteMgr = null;

​    

​    /**

​     \* 私有构造函数

​     */

​    private ServiceHandler()

​    {

​    }

​    

​    /**

​     \* 获取实例

​     \* @return 管理对象

​     */

​    public static synchronized ServiceHandler getInstance()

​    {

​        if (instance == null)

​        {

​            instance = new ServiceHandler();

​        }

​        return instance;

​    }

​    

​    public ISiteMgr getSiteMgr()

​    {

​        return siteMgr;

​    }

​    

​    public void setSiteMgr(final ISiteMgr siteMgr)

​    {

​        this.siteMgr = siteMgr;

​        SiteMgrROAServiceImpl.setSiteMgr(siteMgr);

​    }

​    

}

 

 

========================================================================================================深化===============================================================================================

 

 

前台ajax发送Rest请求------------------------> 服务层，服务层分为 @controller层<处理请求>，业务处理层<处理业务>

 

@controller层 又分为2层   Wrapper层与RoaService层    Wrapper层只接受外部请求，透传请求到RoaService层

Wrapper层：

！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！//只接受外部请求

​    INeauthService neauthService;   //通过接口创建实例  服务转换接口： 前端请求通过该接口转到ROA服务处理类

​    @POST

​    public final void doPOST(HttpContext context)

​    {

​        if (null == neauthService)

​        {

​            getneauthService();

​        }

​        neauthService.setAuth(context);  

​    }

​    

RoaService层：   服务层一定要有个接口

！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！//服务转换接口： 前端请求通过该接口转到ROA服务处理类

public interface INeauthService

{

​    PageModel<NeauthModel> query(HttpContext context);

 

​    void setAuth(HttpContext context);

 

​    void getAuth(HttpContext context);  

}

！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！//前台请求实际处理类，处理请求但不处理业务

public class NeauthROAServiceImpl implements INeauthService

{

 

​        private static INeauthMgr neauthMgr = null;  //==================================================RoaService层 注入 业务处理层，注入不同的业务

​        private static ISiteMgr siteMgr = null;

​        // 解析参数并校验

​        final HttpServletRequest request = context.getHttpServletRequest();

​        final String jsonString = request.getParameter("condition");

​        // 操作数据

​        return neauthMgr.query(condition);

}

 

业务处理层：

局点管理接口

public interface ISiteMgr

{

 

}

网元管理接口

public interface INeauthMgr

{

 

}

局点管理接口实现类！！！！！！！！！！！！！！！！！！！！！//只做业务逻辑的转换、处理，不直接操作数据库

public class SiteMgr implements ISiteMgr

{

​       private final SiteMgrDao dao = SiteMgrDao.getInstance();//=========================================业务处理层 注入 Dao层，注入不同的Dao层

​       private final NeauthDao dao2 = NeauthDao.getInstance();   //一个Dao实例只能处理一个模块

​       

​       

​       final List<SiteModel> siteModels = dao.queryPageSites(siteInfo);

​       

}

 

这两个接口放在API包里，as包依赖API，  只有API能被依赖，as不能被依赖，因为API里放一些公共的东西，要发布出去

接口的实现类放在as包里

 

Dao层：

Dao层分为2层  Dao层数据处理层与Dao层服务层

Dao层数据处理层负责将业务层的数据转换成一般形式Map<String,Object>,或将Dao层服务层返回的Dataset类型转换为业务处理层所需的数据格式

Dao层数据处理层：

public class SiteMgrDao

{

   public int queryPageSites(final SiteModel siteModel){

​            Map<String, Object> map = siteModel.convertModelToMap();

​            siteList.add(map);

​            return DBPersistenceService.insert(TBLNAME, siteList);

   }

}

 

Dao层服务层：适用于处理所有类型的数据

public interface DBPersistenceService{

 

}

 

 

 

表现层Ajax---------------------》服务层，服务层分为controller层与业务处理层，请求处理与业务处理

​                                 controller层分为Wrapper层和RoaService层，或者叫请求接受层，请求处理层，Wrapper层接受外部请求，接受GET.POST.PUT.DEL，RoaService层处理请求，RoaService层 注入 业务处理层，可以注入不同的业务，

​                                 需要调用已发布的公共接口，

​                                 所以RoaService层需要用接口，注入不同的业务通过接口

 

​                                 业务处理层 负责写已调用发布的公共接口的实现类，只做业务逻辑的转换、处理，不直接操作数据库

 

服务层    ---------------------》Dao层，Dao层分为2层  Dao层数据处理层与Dao层服务层，Dao层数据处理层负责将业务层的数据转换成一般形式Map<String,Object>,

​                                 或将Dao层服务层返回的Dataset类型转换为业务处理层所需的数据格式

 

​                                

我:

==================================================================================================ID生成器================================================================================================

 

public abstract class PkidGenerator

{

​    private static AtomicLong startIndex = new AtomicLong(System.currentTimeMillis());

​    

​    /**

​     \* 获取唯一ID

​     \* @return ID

​     */

​    public static long getGenerateId()

​    {

​        return startIndex.incrementAndGet();

​    }

}

我:

==================================================================================================文件操作  文件处理================================================================================================

 

package enterprise.app.securecenter.api.common;

 

import java.io.File;

import java.io.IOException;

import java.util.Calendar;

 

import com.huawei.oms.log.OMSLog;

import com.huawei.oms.log.OMSLogFactory;

import com.huawei.oms.util.OmsConstant;

 

/**

\* Sec文件处理<br>

\* <br>

*

\* @author

\* @version  [eSight SecpolicyMgr V2R3C01, 2013-3-7]

\* @see

\* @since  [eSight SecpolicyMgr V2R3C01]

*/

public abstract class SecFileUtil

{

​    /**

​     \* 路径分隔符

​     */

​    public static final String FILE_SEPARATOR = "/";

​    

​    /**

​     \* 临时目录

​     */

​    public static final String TEMP_DIR = "secpolicy/deployResult/";

​    

​    /**

​     \* 一个小时的秒

​     */

​    public static final long FILE_EXIST_TIME = 3600000;

​    

​    /**

​     \* 文件后缀

​     */

​    public static final String POSTFIX_CSV = ".csv";

​    

​    private static final OMSLog LOGGER = OMSLogFactory.getLog(SecFileUtil.class);

​    

​    /**

​     \* 在目录dir下查找生成时间和现在的时间差大于millSecond的文件，并删除<br>

​     \* @author

​     \* @see

​     \* @since Secospace VSM V2R1, Jan 11, 2012

​     \* @param millSecond 秒

​     \* @param dir 文件夹路径

​     \* @param postfix 文件后缀，如.csv

​     \* @return 返回是否删除成功

​     */

​    public static boolean delteResultFile(final long millSecond, String dir, final String postfix)

​    {

​        final long curTime = Calendar.getInstance().getTimeInMillis();

​        // 如果dir不以文件分隔符结尾，自动添加文件分隔符

​        if (!dir.endsWith(File.separator) && !dir.endsWith(FILE_SEPARATOR))

​        {

​            dir = dir + File.separator;

​        }

​        final File dirFileSec = new File(dir);

​        // 如果dir对应的文件不存在，或者不是一个目录，则退出

​        if (!dirFileSec.exists() || !dirFileSec.isDirectory())

​        {

​            LOGGER.info("delete directory failed Directory is not exsit!");

​            return false;

​        }

​        boolean flag = true;

​        // 删除文件夹下的所有文件(包括子目录)

​        final File[] files = dirFileSec.listFiles();

​        if (files != null)

​        {

​            for (File file : files)

​            {

​                // 判断是子文件，同时现在的时间减去文件的生成时间>millSecond; 删除子文件

​                

​                if (isFileNeedDelete(file, millSecond, curTime, postfix))

​                {

​                    try

​                    {

​                        flag = deleteFile(file.getCanonicalPath());

​                    }

​                    catch (final IOException e)

​                    {

​                        LOGGER.error("delete dir failed");

​                    }

​                    if (!flag)

​                    {

​                        break;

​                    }

​                }

​            }

​        }

​        

​        if (!flag)

​        {

​            LOGGER.info("delete dir failed");

​            return false;

​        }

​        return true;

​    }

​    

​    private static boolean isFileNeedDelete(final File file, final long millSecond, final long curTime,

​        final String postfix)

​    {

​        final boolean result =

​            file.isFile() && ((curTime - file.lastModified()) > millSecond) && isFilePostFixRight(file, postfix);

​        return result;

​    }

​    

​    private static boolean isFilePostFixRight(final File file, final String postfix)

​    {

​        return file.getName().endsWith(postfix);

​    }

​    

​    /**

​     \* 删除目录（文件夹）以及目录下的文件<br>

​     \* @param dir 被删除目录的文件路径

​     \* @return 目录删除成功返回true,否则返回false

​     */

​    /*

​    public static boolean deleteDirectory(String dir)

​    {

​        // 如果dir不以文件分隔符结尾，自动添加文件分隔符

​        if (!dir.endsWith(File.separator) && !dir.endsWith(FILE_SEPARATOR))

​        {

​            dir = dir + File.separator;

​        }

​        final File dirFile = new File(dir);

​        // 如果dir对应的文件不存在，或者不是一个目录，则退出

​        if (!dirFile.exists() || !dirFile.isDirectory())

​        {

​            LOGGER.info("delete directory failed Directory is not exsit!");

​            return false;

​        }

​        boolean flag = true;

​        // 删除文件夹下的所有文件(包括子目录)

​        final File[] files = dirFile.listFiles();

​        if (files != null)

​        {

​            for (File file : files)

​            {

​                // 删除子文件

​                try

​                {

​                    if (file.isFile())

​                    {

​                        flag = deleteFile(file.getCanonicalPath());

​                        if (!flag)

​                        {

​                            break;

​                        }

​                    }

​                    // 删除子目录

​                    else

​                    {

​                        flag = deleteDirectory(file.getCanonicalPath());

​                        if (!flag)

​                        {

​                            break;

​                        }

​                    }

​                }

​                catch (final IOException e)

​                {

​                    LOGGER.error("delete file or dir error");

​                }

​            }

​        }

​        

​        if (!flag)

​        {

​            LOGGER.info("delete dir failed");

​            return false;

​        }

​        

​        // 删除当前目录

​        if (dirFile.delete())

​        {

​            LOGGER.info("delete dir successed!");

​            return true;

​        }

​        else

​        {

​            LOGGER.info("delete dir failed!");

​            return false;

​        }

​    }

我:

*/

​    /**

​     \* 删除单个文件<br>

​     \* @param fileName 被删除文件的文件名

​     \* @return 单个文件删除成功返回true,否则返回false

​     */

​    public static boolean deleteFile(final String fileName)

​    {

​        final File file = new File(fileName);

​        if (file.isFile() && file.exists())

​        {

​            final boolean result = file.delete();

​            LOGGER.info("delete single file");

​            return result;

​        }

​        else

​        {

​            return true;

​        }

​    }

​    

​    /**

​     \* 　 生成文件的绝对路径{版本安装路径}\var\iemp\storage\secpolicy\deployResult\19858156372667/Eudemon1000E-N7E_10.137.240.57_result.zip

​     *

​     \* @param prefix 文件名前缀,如果文件名中包含特殊字符，如"\,?,空白"，都会替换成"_"

​     \* @param suffix  文件后缀名,比如：.txt .csv .xml

​     \* @param specifiedFileName  如果不填就用当前时间生成一个文件名，如果填了就会使用填的文件名并且生成一个以当前时间为名字的文件夹

​     \* @param systemTime  系统时间

​     \* @return 文件的绝对路径

​     */

​    public static String getAbsoluteFileName(final String prefix, final String suffix, final String specifiedFileName,

​        final String systemTime)

​    {

​        final String absolutePath = getAbsoluteFilePath();

​        

​        final File tempFileDir = new File(absolutePath);

​        

​        if (!tempFileDir.exists())

​        {

​            if (!tempFileDir.mkdirs())

​            {

​                LOGGER.error("mkdirs failed,all ready exist! " + absolutePath);

​            }

​        }

​        

​        final StringBuilder absolutePathName = new StringBuilder();

​        

​        absolutePathName.append(absolutePath)

​            .append(escapseFileName(prefix, "_"))

​            .append(specifiedFileName)

​            .append("_")

​            .append(systemTime)

​            .append(suffix);

​        

​        return absolutePathName.toString();

​    }

​    

​    /**

​     \* 　 生成 路径文件的相对路径：

​     \* 附件对应的路径信息 ，最多100个字符。即该日志对应的附件的相对路径，如果无附件，该字段为空。

​     \* 最终路径为：{版本安装路径}\var\iemp\storage\{attachment指定的路径}。

​     \* @param prefix  文件名前缀

​     \* @param suffix   文件后缀名,比如：.txt .csv .xml

​     \* @param specifiedFileName  如果不填就用当前时间生成一个文件名，如果填了就会使用填的文件名并且生成一个以当前时间为名字的文件夹

​     \* @param systemTime   记录的文件时间

​     \* @return 生成 路径文件的相对路径

​     */

​    public static String getRelativeFileName(final String prefix, final String suffix, final String specifiedFileName,

​        final String systemTime)

​    {

​        final String relativePath = getRelativeFilePath(prefix, suffix, specifiedFileName, systemTime);

​        

​        return relativePath.replaceAll("(?i)\\.txt$", ".zip");

​    }

​    

​    private static String getRelativeFilePath(final String prefix, final String suffix, final String specifiedFileName,

​        final String systemTime)

​    {

​        final StringBuilder relativeFilePath = new StringBuilder(TEMP_DIR);

​        

​        relativeFilePath.append(escapseFileName(prefix, "_"))

​            .append(specifiedFileName)

​            .append("_")

​            .append(systemTime)

​            .append(suffix);

​        

​        return relativeFilePath.toString();

​    }

​    

​    /**

​     \* getAbsoluteFilePath

​     \* @return path

​     */

​    public static String getAbsoluteFilePath()

​    {

​        String temPath = "";

​        

​        temPath =

​            System.getProperty(OmsConstant.OMS_PATH_VAR) == null ? "" : System.getProperty(OmsConstant.OMS_PATH_VAR);

​        

​        LOGGER.info("the temPath is " + temPath);

​        

​        if (temPath != null)

​        {

​            return temPath.concat(File.separator)

​                .concat("storage")

​                .concat(File.separator)

​                .concat("secpolicy")

​                .concat(File.separator)

​                .concat("deployResult")

​                .concat(File.separator);

​        }

​        else

​        {

​            return "";

​        }

​    }

​    

​    /**

​     \* 替换操作系统创建文件的敏感字符

​     \* @param str  输入字符串

​     \* @param repStr 替换的字符

​     \* @return 替换后的字符串

​     */

​    private static String escapseFileName(String str, final String repStr)

​    {

​        str = str.replace("\\", repStr);

​        str = str.replace("/", repStr);

​        str = str.replace(":", repStr);

​        str = str.replace("*", repStr);

​        str = str.replace("?", repStr);

​        str = str.replace("\"", repStr);

​        str = str.replace("<", repStr);

​        str = str.replace(">", repStr);

​        str = str.replace("|", repStr);

​        

​        str = str.replace(" ", "_");

​        return str;

​    }

​    

}

我:

==================================================================================================文件压缩================================================================================================

\* 用于将文件转换为ZipString的类

\* @author j00218878

*

*/

public class ZipUtils

{

​    

​    private static final Logger LOGGER = OMSLogFactory.getLog(ZipUtils.class);

​    

​    private static final int BUFFER = 2048;

​    

​    private static final ZipUtils INST = new ZipUtils();

​    

​    // 压缩包中的文件名编码格式暂定为gbk

​    private static final String FILENAME_ENCODING = "GBK";

​    

​    public static ZipUtils getInst()

​    {

​        return INST;

​    }

​    

​    /**

​     \* 压缩多个文件到一个zip中

​     \* @param files  要压缩的文件列表

​     \* @param destFilePath  要压缩到的zip文件名

​     */

​    public void zip(final List<String> files, final String destFilePath)

​    {

​        BufferedInputStream bin = null;

​        ZipOutputStream zout = null;

​        FileOutputStream out = null;

​        BufferedOutputStream bout = null;

​        InputStream in = null;

​        

​        try

​        {

​            final File destFile = new File(destFilePath);

​            if (/**FortifyUtil.isInSecureDir(destFile) && **/

​            FortifyUtil.isRegularFile(destFile))

​            {

​                out = FortifyUtil.newFileOutputStream(destFile);

​                bout = new BufferedOutputStream(out);

​                zout = new ZipOutputStream(bout);

​                // 改用ant的zip后设置文件名的编码方式

​                zout.setEncoding(FILENAME_ENCODING);

​                

​                for (final String srcFilePath : files)

​                {

​                    try

​                    {

​                        final byte data[] = new byte[BUFFER];

​                        final File srcFile = FortifyUtil.newFile(srcFilePath);

​                        if (/**FortifyUtil.isInSecureDir(srcFile) && **/

​                        FortifyUtil.isRegularFile(srcFile))

​                        {

​                            in = FortifyUtil.newFileInputStream(srcFile);

​                            bin = new BufferedInputStream(in);

​                            

​                            final ZipEntry entry = new ZipEntry(new File(srcFilePath).getName());

​                            zout.putNextEntry(entry);

​                            int count;

​                            

​                            while ((count = bin.read(data, 0, BUFFER)) != -1)

​                            {

​                                zout.write(data, 0, count);

​                            }

​                        }

​                    }

​                    finally

​                    {

​                        IOUtils.close(bin, in);

​                    }

​                }

​            }

​        }

​        catch (final IOException ioException)

​        {

​            LOGGER.error("Compress files [" + files.size() + "] to destFile:" + destFilePath + "failed.", ioException);

​        }

​        finally

​        {

​            IOUtils.close(zout, bout, out);

​        }

​    }

​    

​    /**

​     \* 压缩文件

​     *

​     \* @param srcFilePath

​     \*            源文件路径

​     \* @param destFilePath

​     \*            目标文件路径

​     *

​     */

​    public void zip(final String srcFilePath, final String destFilePath)

​    {

​        final List<String> zipArr = new ArrayList<String>(1);

​        zipArr.add(srcFilePath);

​        

​        zip(zipArr, destFilePath);

​    }

​    

}

我:

==================================================================================================约束类型================================================================================================

 

/**

\* 约束类型

*

\* @author t00201981

*

*/

public enum ConstraintType

{

​    /**

​     \* 等于

​     */

​    equal

​    {

​        /**

​         \* {@inheritDoc}

​         */

​        @Override

​        public boolean isStatisfy(Object paramObject1, Object paramObject2)

​        {

​            if (paramObject1 == null)

​            {

​                return paramObject2 == null;

​            }

​            return paramObject1.equals(paramObject2);

​        }

​    },

​    

​    /**

​     \* 大于

​     */

​    greater

​    {

​        /**

​         \* {@inheritDoc}

​         */

​        @Override

​        public boolean isStatisfy(Object paramObject1, Object paramObject2)

​        {

​            if (paramObject1 instanceof Number)

​            {

​                Number x = (Number)paramObject1;

​                Number y = (Number)paramObject2;

​                return x.doubleValue() > y.doubleValue();

​            }

​            if (paramObject1 instanceof Date)

​            {

​                return ((Date)paramObject1).after((Date)paramObject2);

​            }

​            if (paramObject1 instanceof Character)

​            {

​                return ((Character)paramObject1).charValue() > ((Character)paramObject2).charValue();

​            }

​            return false;

​        }

​    },

​    

​    /**

​     \* 小于

​     */

​    smaller

​    {

​        /**

​         \* {@inheritDoc}

​         */

​        @Override

​        public boolean isStatisfy(Object paramObject1, Object paramObject2)

​        {

​            if (paramObject1 instanceof Number)

​            {

​                Number x = (Number)paramObject1;

​                Number y = (Number)paramObject2;

​                return x.doubleValue() < y.doubleValue();

​            }

​            if (paramObject1 instanceof Date)

​            {

​                return ((Date)paramObject1).before((Date)paramObject2);

​            }

​            if (paramObject1 instanceof Character)

​            {

​                return ((Character)paramObject1).charValue() < ((Character)paramObject2).charValue();

​            }

​            return false;

​        }

​    },

​    

​    /**

​     \* 模糊匹配

​     */

​    like

​    {

​        /**

​         \* {@inheritDoc}

​         */

​        @Override

​        public boolean isStatisfy(Object paramObject1, Object paramObject2)

​        {

​            return String.valueOf(paramObject1).toUpperCase().contains(String.valueOf(paramObject2).toUpperCase());

​        }

​    },

​    

​    /**

​     \* 不等于

​     */

​    notEqual

​    {

​        /**

​         \* {@inheritDoc}

​         */

​        @Override

​        public boolean isStatisfy(Object paramObject1, Object paramObject2)

​        {

​            return !equal.isStatisfy(paramObject1, paramObject2);

​        }

​    },

​    

​    /**

​     \* 小于等于

​     */

​    notGreater

​    {

​        /**

​         \* {@inheritDoc}

​         */

​        @Override

​        public boolean isStatisfy(Object paramObject1, Object paramObject2)

​        {

​            return !greater.isStatisfy(paramObject1, paramObject2);

​        }

​    },

​    

​    /**

​     \* 大于等于

​     */

​    notSmaller

​    {

​        /**

​         \* {@inheritDoc}

​         */

​        @Override

​        public boolean isStatisfy(Object paramObject1, Object paramObject2)

​        {

​            return !smaller.isStatisfy(paramObject1, paramObject2);

​        }

​    },

​    

​    /**

​     \* 完全不匹配

​     */

​    notLike

​    {

​        /**

​         \* {@inheritDoc}

​         */

​        @Override

​        public boolean isStatisfy(Object paramObject1, Object paramObject2)

​        {

​            return !like.isStatisfy(paramObject1, paramObject2);

​        }

​    },

​    

​    /**

​     \* 与

​     */

​    and

​    {

​        /**

​         \* {@inheritDoc}

​         */

​        @Override

​        public boolean isStatisfy(Object paramObject1, Object paramObject2)

​        {

​            return false;

​        }

​    },

​    

​    /**

​     \* 或

​     */

​    or

​    {

​        /**

​         \* {@inheritDoc}

​         */

​        @Override

​        public boolean isStatisfy(Object paramObject1, Object paramObject2)

​        {

​            return false;

​        }

​    },

​    

​    /**

​     \* 包含于

​     */

​    in

​    {

​        /**

​         \* {@inheritDoc}

​         */

​        @Override

​        public boolean isStatisfy(Object paramObject1, Object paramObject2)

​        {

​            if (paramObject2 instanceof Object[])

​            {

​                Object[] exceptValues = (Object[])paramObject2;

​                for (Object o : exceptValues)

​                {

​                    if (equal.isStatisfy(paramObject1, o))

​                    {

​                        return true;

​                    }

​                }

​            }

​            else if (paramObject2 instanceof Collection<?>)

​            {

​                Collection<?> exceptValues = (Collection<?>)paramObject2;

​                for (Object o : exceptValues)

​                {

​                    if (equal.isStatisfy(paramObject1, o))

​                    {

​                        return true;

​                    }

​                }

​            }

​            return false;

​        }

​    },

​    

​    /**

​     \* 不包含于

​     */

​    notIn

​    {

​        /**

​         \* {@inheritDoc}

​         */

​        @Override

​        public boolean isStatisfy(Object paramObject1, Object paramObject2)

​        {

​            return !in.isStatisfy(paramObject1, paramObject2);

​        }

​    },

​    

​    /**

​     \* 包含

​     */

​    contain

​    {

​        /**

​         \* {@inheritDoc}

​         */

​        @Override

​        public boolean isStatisfy(Object paramObject1, Object paramObject2)

​        {

​            if (paramObject1 instanceof Object[])

​            {

​                Object[] exceptValues = (Object[])paramObject1;

​                for (Object o : exceptValues)

​                {

​                    if (equal.isStatisfy(paramObject2, o))

​                    {

​                        return true;

​                    }

​                }

​            }

​            else if (paramObject1 instanceof Collection<?>)

​            {

​                Collection<?> exceptValues = (Collection<?>)paramObject1;

​                for (Object o : exceptValues)

​                {

​                    if (equal.isStatisfy(paramObject2, o))

​                    {

​                        return true;

​                    }

​                }

​            }

​            return false;

​        }

​    },

​    

​    /**

​     \* 不包含

​     */

​    notContain

​    {

​        /**

​         \* {@inheritDoc}

​         */

​        @Override

​        public boolean isStatisfy(Object paramObject1, Object paramObject2)

​        {

​            return !contain.isStatisfy(paramObject1, paramObject2);

​        }

​    };

​    

​    /**

​     \* 是否满足

​     \* @param paramObject1 被匹配对象

​     \* @param paramObject2 匹配对象

​     \* @return 是否满足

​     */

​    protected abstract boolean isStatisfy(Object paramObject1, Object paramObject2);

}

我:

==================================================================================================查询条件================================================================================================

\* 查询条件

*

\* @author t00201981

*

*/

\* @param type 约束类型

\* @param field 字段名

\* @param paramObject 查询参数

public class Constraint

{

​    private ConstraintType type;

​    

​    private String field;

​    

​    private Object paramObject;

}

 

 

/**

\* 查询条件

*

\* @author t00201981

*

*/

public class Criterion

{

​    /**

​     \* 日志

​     */

​    private static final OMSLog LOGGER = OMSLogFactory.getLog(Criterion.class);

​    

​    /**

​     \* and/or后面一个查询条件

​     */

​    private Criterion nextCriterion;

​    

​    /**

​     \* and/or查询条件

​     */

​    private ConstraintType logicType;

​    

​    /**

​     \* 约束条件

​     */

​    private Constraint constraint;

​    

​    /**

​     \* 排序类型：升序或降序

​     */

​    private OrderType orderType;

​    

​    /**

​     \* 排序字段

​     */

​    private List<String> orderField;

​    

​    /**

​     \* 模糊匹配

​     \* @param field 字段名

​     \* @param paramObject 匹配对象

​     \* @return 查询条件

​     */

​    public static Criterion like(String field, Object paramObject)

​    {

​        return createCriterion(ConstraintType.like, field, paramObject);

​    }

​    

​    /**

​     \* 等于

​     \* @param field 字段名

​     \* @param paramObject 匹配对象

​     \* @return 查询条件

​     */

​    public static Criterion equal(String field, Object paramObject)

​    {

​        return createCriterion(ConstraintType.equal, field, paramObject);

​    }

​    

​    /**

​     \* 大于

​     \* @param field 字段名

​     \* @param paramObject 匹配对象

​     \* @return 查询条件

​     */

​    public static Criterion greater(String field, Object paramObject)

​    {

​        return createCriterion(ConstraintType.greater, field, paramObject);

​    }

​    

​    /**

​     \* 小于

​     \* @param field 字段名

​     \* @param paramObject 匹配对象

​     \* @return 查询条件

​     */

​    public static Criterion smaller(String field, Object paramObject)

​    {

​        return createCriterion(ConstraintType.smaller, field, paramObject);

​    }

​    

​    /**

​     \* 包含于

​     \* @param field 字段名

​     \* @param paramObject 匹配对象

​     \* @return 查询条件

​     */

​    public static Criterion in(String field, Object paramObject)// NOPMD by t00201981

​    {

​        return createCriterion(ConstraintType.in, field, paramObject);

​    }

​    

​    /**

​     \* 包含

​     \* @param field 字段名

​     \* @param paramObject 匹配对象

​     \* @return 查询条件

​     */

​    public static Criterion contain(String field, Object paramObject)

​    {

​        return createCriterion(ConstraintType.contain, field, paramObject);

​    }

​    

​    /**

​     \* 不相等

​     \* @param field 字段名

​     \* @param paramObject 匹配对象

​     \* @return 查询条件

​     */

​    public static Criterion notEqual(String field, Object paramObject)

​    {

​        return createCriterion(ConstraintType.notEqual, field, paramObject);

​    }

​    

​    /**

​     \* 小于等于

​     \* @param field 字段名

​     \* @param paramObject 匹配对象

​     \* @return 查询条件

​     */

​    public static Criterion notGreater(String field, Object paramObject)

​    {

​        return createCriterion(ConstraintType.notGreater, field, paramObject);

​    }

​    

​    /**

​     \* 大于等于

​     \* @param field 字段名

​     \* @param paramObject 匹配对象

​     \* @return 查询条件

​     */

​    public static Criterion notSmaller(String field, Object paramObject)

​    {

​        return createCriterion(ConstraintType.notSmaller, field, paramObject);

​    }

​    

​    /**

​     \* 完全不匹配

​     \* @param field 字段名

​     \* @param paramObject 匹配对象

​     \* @return 查询条件

​     */

​    public static Criterion notLike(String field, Object paramObject)

​    {

​        return createCriterion(ConstraintType.notLike, field, paramObject);

​    }

​    

​    /**

​     \* 不包含于

​     \* @param field 字段名

​     \* @param paramObject 匹配对象

​     \* @return 查询条件

​     */

​    public static Criterion notIn(String field, Object paramObject)

​    {

​        return createCriterion(ConstraintType.notIn, field, paramObject);

​    }

​    

​    /**

​     \* 不包含

​     \* @param field 字段名

​     \* @param paramObject 匹配对象

​     \* @return 查询条件

​     */

​    public static Criterion notContain(String field, Object paramObject)

​    {

​        return createCriterion(ConstraintType.notContain, field, paramObject);

​    }

​    

​    /**

​     \* 创建查询条件

​     \* @param constraintType 约束类型

​     \* @param field 字段名

​     \* @param paramObject 匹配对象

​     \* @return 查询条件

​     */

​    public static Criterion createCriterion(ConstraintType constraintType, String field, Object paramObject)

​    {

​        Criterion criterion = new Criterion();

​        criterion.constraint = new Constraint(constraintType, field, paramObject);

​        return criterion;

​    }

​    

​    /**

​     \* 与

​     \* @param criterion 查询条件

​     \* @return 查询条件

​     */

​    public Criterion and(Criterion criterion)

​    {

​        if (this.nextCriterion == null)

​        {

​            this.nextCriterion = criterion;

​            this.logicType = ConstraintType.and;

​        }

​        else

​        {

​            nextCriterion.and(criterion);

​        }

​        

​        return this;

​    }

​    

​    /**

​     \* 或

​     \* @param criterion 查询条件

​     \* @return 查询条件

​     */

​    public Criterion or(Criterion criterion)// NOPMD by t00201981

​    {

​        if (this.nextCriterion == null)

​        {

​            this.nextCriterion = criterion;

​            this.logicType = ConstraintType.or;

​        }

​        else

​        {

​            nextCriterion.or(criterion);

​        }

​        

​        return this;

​    }

​    

​    /**

​     \* 升序排序

​     \* @param field 字段名

​     \* @return 查询条件

​     */

​    public Criterion orderAsc(String... field)

​    {

​        orderType = OrderType.Asc;

​        orderField = Arrays.asList(field);

​        return this;

​    }

​    

​    /**

​     \* 降序排序

​     \* @param field 字段名

​     \* @return 查询条件

​     */

​    public Criterion orderDesc(String... field)

​    {

​        orderType = OrderType.Desc;

​        orderField = Arrays.asList(field);

​        return this;

​    }

​    

​    /**

​     \* 是否满足条件

​     \* @param object 被匹配对象

​     \* @return 查询条件

​     \* @throws ServiceException 异常

​     */

​    public boolean isSatisfy(Object object)

​        throws ServiceException

​    {

​        try

​        {

​            Object prop = PropertyUtils.getNestedProperty(object, constraint.getField());

​            

​            boolean result = constraint.getType().isStatisfy(prop, constraint.getParamObject());

​            

​            if (nextCriterion == null)

​            {

​                return result;

​            }

​            else

​            {

​                if (ConstraintType.and.equals(logicType))

​                {

​                    return result && nextCriterion.isSatisfy(object);

​                }

​                else if (ConstraintType.or.equals(logicType))

​                {

​                    return result || nextCriterion.isSatisfy(object);

​                }

​                else

​                {

​                    return result;

​                }

​            }

​        }

​        catch (IllegalAccessException e)

​        {

​            throw new ServiceException(e);

​        }

​        catch (InvocationTargetException e)

​        {

​            throw new ServiceException(e);

​        }

​        catch (NoSuchMethodException e)

​        {

​            throw new ServiceException(e);

​        }

​    }

​    

​    /**

​     \* 排序

​     \* @param <E> 排序对象类型

​     \* @param <T> 排序字段类型

​     \* @param list 排序集合

​     */

​    public <E, T> void order(List<E> list)

​    {

​        if ((orderField == null) || orderField.isEmpty())

​        {

​            return;

​        }

​        for (final String fieldName : orderField)

​        {

​            Comparator<E> comparator = new Comparator<E>()

​            {

​                @SuppressWarnings("unchecked")

​                @Override

​                public int compare(Object o1, Object o2)

​                {

​                    try

​                    {

​                        Object prop1 = PropertyUtils.getNestedProperty(o1, fieldName);

​                        Object prop2 = PropertyUtils.getNestedProperty(o2, fieldName);

​                        if (prop1 instanceof Comparable<?>)

​                        {

​                            return ((Comparable<T>)prop1).compareTo((T)prop2);

​                        }

​                        else

​                        {

​                            return String.valueOf(prop1).compareTo(String.valueOf(prop2));

​                        }

​                    }

​                    catch (IllegalAccessException e)

​                    {

​                        LOGGER.error("Illegal Access Exception", e);

​                        return 0;

​                    }

​                    catch (InvocationTargetException e)

​                    {

​                        LOGGER.error("Invocation Target Exception", e);

​                        return 0;

​                    }

​                    catch (NoSuchMethodException e)

​                    {

​                        LOGGER.error("No Such Method Exception", e);

​                        return 0;

​                    }

​                }

​            };

​            

​            if (OrderType.Desc.equals(orderType))

​            {

​                comparator = Collections.reverseOrder(comparator);

​            }

​            

​            Collections.sort(list, comparator);

​        }

​        

​    }

}

我:

==================================================================================================Set与List================================================================================================

​    public static Set<String> convertStrValue2Set(final String str)

​    {

​        final Set<String> valueList = new LinkedHashSet<String>();  

​        if (StringUtils.isNotEmpty(str))

​        {

​            final String[] splitValue = str.split(",");

​            valueList.addAll(Arrays.asList(splitValue));     //自带一个功能 去除重复

​        }

​        return valueList;

​    }

 

​    public static List<String> convertStrValue2List(final String str)

​    {

​        final List<String> valueList = new LinkedList<String>();

​        if (StringUtils.isNotEmpty(str))

​        {

​            final String[] splitValue = str.split(",");

​            valueList.addAll(Arrays.asList(splitValue));   //没有去除重复的功能

​        }

​        

​        return valueList;

​    }

 

==================================================================================================正则================================================================================================

​        final Pattern pattern = Pattern.compile(regexStr);

​        final Matcher nameMatcher = pattern.matcher(str);

​        if (!nameMatcher.matches())

​        

​        

==================================================================================================判断是否是0================================================================================================        

​    public static boolean isZero(final Object obj)

​    {

​        if ((obj instanceof Long) || (obj instanceof Integer))

​        {

​            if (Long.parseLong(obj.toString()) == 0)

​            {

​                return true;

​            }

​        }

​        return false;

​    }        

​        

==================================================================================================================================================================================================            

​        

​    public static void main(String[] args)

​    {

​        List<Book> bL = new ArrayList<Book>();

​        int i=1;

​        while(i<=2){

​            Book bk = null;

​            bk.setId(i);   //会报空指针异常  为什么？  因为Book bk = null;  则bk.setId  没这个方法

​            bL.add(bk);

​            i++;

​        }

​        System.out.println(bL.size());

​    }        

​        

=================================================================================================枚举================================================================================================        

​    public static String getValue(final String key)

​    {

​        final EnumSet<EnumNatMode> enumSet = EnumSet.allOf(EnumNatMode.class);

​        for (final EnumNatMode enmu : enumSet)

​        {

​            if (enmu.key.equals(key))

​            {

​                return enmu.value;

​            }

​        }

​        return "";

​    }        

=================================================================================================适配的思想================================================================================================    

 

一方法需要返回DataSet类型，可是现在的方法实际返回List<DataSet>

/**

\* 多个data set适配

\* @author t00201981

*

*/

public class MultiDataSetAdapter implements DataSet

{

​    private final List<DataSet> setList;

​    private int curIndex = 0;

}

public MultiDataSetAdapter(List<DataSet> setList)

{

​    this.setList = setList;

}

@Override

public float getFloat(String paramString)

{

​    return setList.get(curIndex).getFloat(paramString);

}

@Override

public boolean next()

{

​        if (setList.get(curIndex).next())

​        {

​            return true;

​        }

​        else if (curIndex < setList.size() - 1)

​        {

​            curIndex++;

​            return next();

​        }

​        return false;

}

我:

=================================================================================================枚举的用法2================================================================================================    

public enum EnumStatus

{

​    /**

​     \* 任务状态：进行中

​     */

​    RUN(1),

​    

​    /**

​     \* 任务状态：已完成

​     */

​    END(2);

​    

​    private int status;

​    

​    EnumStatus(final int status)

​    {

​        this.status = status;

​    }

​    

​    public int getStatus()

​    {

​        return status;

​    }

​    

​    public static boolean hasValue(final int status)

​    {

​        EnumStatus[] enumStatus = EnumStatus.values();    //EnumStatus.values()为一个数组，EnumStatus类型

​        for (EnumStatus sts : enumStatus)

​        {

​            if (status == sts.getStatus())

​            {

​                return true;

​            }

​        }

​        return false;

​    }

}

 

 

也即 RUN、END为 EnumStatus的值  EnumStatus.RUN  EnumStatus.END====> EnumStatus.RUN.getStatus()得到值的值

 

 

final int authNO = EnumStatus.RUN.getStatus();     -------------  1

final int authOK = EnumStatus.END.getStatus();     -------------  2

EnumStatus[] enumStatus = EnumStatus.values();    -------------  [RUN,END]

public enum NetBIOSNameType

{

​    /**

​     \* 0x00 WorkStaion Server Name

​     */

​    SERVER_NAME(0),

​    

​    /**

​     \* 0x03 Messenger Service

​     */

​    MAIL_SERVER_NAME(3),

​    

​    /**

​     \* 0x20

​     */

​    FILE_SERVER_NAME(32),

​    

​    /**

​     \* 其他类型

​     */

​    OTHER_HOST_NAME(100);

​    

​    private int nametype;

​    

​    NetBIOSNameType(final int nametype)

​    {

​        this.setNametype(nametype);

​    }

​    

​    public void setNametype(final int nametype)

​    {

​        this.nametype = nametype;

​    }

​    

​    public int getNametype()

​    {

​        return nametype;

​    }

​    

​    /**

​     \* 将int型的主机类型转换成enum类型

​     \* @param hosttype 主机类型的Int值

​     \* @return 转换后的主机类型

​     */

​    public static NetBIOSNameType getNetBIOSNameType(final int hosttype)

​    {

​        final NetBIOSNameType type;

​        switch (hosttype)

​        {

​            case 0:

​                type = NetBIOSNameType.SERVER_NAME;

​                break;

​            case 3:

​                type = NetBIOSNameType.MAIL_SERVER_NAME;

​                break;

​            case 32:

​                type = NetBIOSNameType.FILE_SERVER_NAME;

​                break;

​            default:

​                type = NetBIOSNameType.OTHER_HOST_NAME;

​                break;

​        }

​        return type;

​    }

}

我:

=================================================================================================查询条件数据模型================================================================================================

public class QueryAuthInfo

{

​    /**

​     *当前页

​     */

​    private int currentPage = 1;

​    

​    /**

​     \* 当前页起始索引

​     */

​    private int pageBegin = -1;

​    

​    /**

​     \* 页面显示条数

​     */

​    private int pageSize = -1;

​    

​    private String taskId;

​    /**

​     \* 无参构造器

​     */

​    public QueryAuthInfo()

​    {

​        super();

​    }

​    

​    /**

​     \* 查询条件Map转为QueryAuthInfo

​     \* @param jsonString 前台传入的json字符串

​     */

​    public void convert2Model(final Map<String, Object> params){}

​    

​    /**

​     \* SiteInfo转换为数据库查询条件Map

​     \* @return 数据库查询条件

​     */

​    public Map<String, Object> convertModel2Map(){}

}

我:

=================================================================================================批量更新================================================================================================

 

/**

​     \* 将集合拼接成字符串，eg：  'nedn1','nedn2'

​     \* @param strCollecton str集合

​     \* @return 拼接后的字符串

​     */

​    public static String buildStrByList(final Collection<String> strCollecton)

​    {

​        if (CollectionUtils.isEmpty(strCollecton))

​        {

​            return null;

​        }

​        final StringBuffer sb = new StringBuffer();

​        for (final String str : strCollecton)

​        {

​            sb.append(INVERTEDCOMMA);

​            sb.append(str);

​            sb.append(INVERTEDCOMMA);

​            sb.append(COMMA);

​        }

​        sb.delete(sb.length() - COMMA.length(), sb.length());

​        return sb.toString();

​    }

 

 

=================================================================================================获取序列id================================================================================================

 

​        try

​        {

​        }

​        catch (DASException err)

​        {

 

​        }

​        catch (Exception e)

​        {

 

​        }

​        顺序执行

 

 

 

=================================================================================================匿名内部类================================================================================================

//用在通过接口创建实例   

​        final Thread newThread = new Thread(new Runnable()

​        {

​            @Override

​            public void run()

​            {

​                bindHelper.update();

​            }

​        });

​        

​        深化：

​        通过接口创建实例，通过父类创建子类

​        

​        Son a = new Son();

我:

=================================================================================================Timer、TimerTask================================================================================================

 

​    public static void main(String[] args)

​    {

​        Calendar calendar = Calendar.getInstance();

​        int year = calendar.get(Calendar.YEAR);

​        int month = calendar.get(Calendar.MONTH);

​        int day = calendar.get(Calendar.DATE);

​        calendar.set(year, month, day);   

​        calendar.set(Calendar.HOUR_OF_DAY, 11);

​        calendar.set(Calendar.MINUTE, 27);

​        calendar.set(Calendar.SECOND, 0);

​        Date date = calendar.getTime();

​        Timer timer = new Timer();

​        timer.schedule(new TimerTask(){

​            @Override

​            public void run()

​            {

​                System.out.println(new SimpleDateFormat("yyyy-MM-dd HH:mm:ss").format(new Date()) + " 定时任务开始 草泥马");   

​            }

​            

​        }, date);

​    }

 

=================================================================================================按指定频率周期执行某个任务================================================================================================

​        ScheduledExecutorService  延迟连接池

​    

​        ScheduledExecutorService executor = Executors.newScheduledThreadPool(1);

​        

​        executor.scheduleAtFixedRate(new Runnable(){

​            @Override

​            public void run()

​            {

​                System.out.println("thread start!!!");

​            }

​            

​        }, 0, 1000, TimeUnit.MILLISECONDS); //初始化延迟0ms开始执行，每隔100ms重新执行一次任务

​        

​        

​        executor.execute(Runnable);  //将线程放入池

​        executor.shutdown();

​    

​    

=================================================================================================每天晚上8点执行某任务================================================================================================

​    private static long getTimeMillis(String time)

​    {

​        

​        DateFormat dataFormat = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");

​        

​        DateFormat dayFormat = new SimpleDateFormat("yyyy-MM-dd");

​        

​        try

​        {

​            Date curDate = dataFormat.parse(dayFormat.format(new Date()) + " " +time);

​            

​            return curDate.getTime();

​        }

​        catch (ParseException e)

​        {

​            // TODO Auto-generated catch block

​            e.printStackTrace();

​        }

 

​        return 0;

​    }

​    

​    

​    main(){

​    

​        ScheduledExecutorService executor = Executors.newScheduledThreadPool(1);

​        

​        long oneDay =24*60*60*1000;

​        

​        long initDelay = getTimeMillis("20:00:00") - System.currentTimeMillis();

​        

​        initDelay = initDelay > 0 ? initDelay : initDelay + oneDay;

​        

​        executor.scheduleAtFixedRate(new Runnable(){

​             @Override

​             public void run()

​             {

​               System.out.println("thread start!!!");

​             }

​      

​        }, initDelay, oneDay, TimeUnit.MILLISECONDS);

​        

​        executor.shutdown();

​    }

我:

=================================================================================================创建并执行在给定延迟后启用的任务================================================================================================

ScheduledExecutorService ses = Executors.newSingleThreadScheduledExecutor();

Future<?> future = ses.schedule(Callable<V> callable, 10, TimeUnit.MILLISECONDS);

Future<?> future = ses.schedule(Runnable command, 10, TimeUnit.MILLISECONDS);

 

scheduleAtFixedRate(Runnable command, long initialDelay, long period, TimeUnit unit)

​          创建并执行一个在给定初始延迟后首次启用的定期操作，后续操作具有给定的周期；也就是将在 initialDelay 后开始执行，然后在 initialDelay+period 后执行，接着在 initialDelay + 2 * period 后执行，依此类推。

scheduleWithFixedDelay(Runnable command, long initialDelay, long delay, TimeUnit unit)

​          创建并执行一个在给定初始延迟后首次启用的定期操作，随后，在每一次执行终止和下一次执行开始之间都存在给定的延迟。

 

=================================================================================================返回前台模型================================================================================================

 

public class ReturnModel<T> implements Serializable            //泛型亮了

{

​    /**

​     \* serialVersionUID

​     */

​    private static final long serialVersionUID = -1L;

 

​    /**

​     \* 错误码

​     */

​    private int errorCode;

 

​    /**

​     \* 返回对象

​     */

​    private T results;

 

​    /**

​     \* 无参构造方法

​     */

​    public ReturnModel()

​    {

​    }

​    

​    GET、SET

}

 

 

ROA的返回结果 {resut:"success",data:{"name" : "cxxx"}}

 

 

​    

=====================================================================================================缓存================================================================================================

 

缓存一定是单例的，单例对象的属性一定是 ConcurrentHashMap

 

public class TelnetBuffer

{

​    private static TelnetBuffer buffer = new TelnetBuffer();

​    /**

​     \* 缓存连接

​     */

​    private final ConcurrentHashMap<String, Context> telnetContext = new ConcurrentHashMap<String, Context>();

​    

​    /**

​     \* 缓存并发度

​     */

​    private final ConcurrentHashMap<String, List<String>> connectCount = new ConcurrentHashMap<String, List<String>>();

​    

​    public static TelnetBuffer getInstance()

​    {

​        return buffer;

​    }

}

 

Context context = TelnetBuffer.getInstance().getTelnetContext().get(telnetInfo.getSessionId());

 

 

 

=====================================================================================================ThreadLocal================================================================================================

 

public class TestThreadLocal

{

​    private static final ThreadLocal<Integer> value = new ThreadLocal<Integer>(){

​        @Override

​        protected Integer initialValue()

​        {

​            return 0;

​        }

​    };

​    

​    public static void main(String[] args)

​    {

​        for(int i=0;i<5;i++){

​            new Thread(new MyThread(i)).start();

​        }

​    }

​    

​    static class MyThread implements Runnable{

​        private int index;

​        

​        public MyThread(int index){

​            this.index = index;

​        }

 

​        @Override

​        public void run()

​        {

​            System.out.println("线程"+ index + "的初始value：" + value.get());

​            for(int i=0;i<10;i++){

​                value.set(value.get()+i);

​            }

​            System.out.println("线程"+ index + "的累加value：" + value.get());

​            

​            //对于ThreadLocal使用前或者使用后一定要先remove

​            value.remove();

​        }

​    }

}

 

线程1的初始value：0

线程2的初始value：0

线程3的初始value：0

线程4的初始value：0

线程0的初始value：0

线程4的累加value：45

线程3的累加value：45

线程2的累加value：45

线程1的累加value：45

线程0的累加value：45

我:

 

 

简单说ThreadLocal就是一种以空间换时间的做法，在每个Thread里面维护了一个以开地址法实现的ThreadLocal.ThreadLocalMap，把数据进行隔离，数据不共享，自然就没有线程安全方面的问题了

 

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

对于ThreadLocal使用前或者使用后一定要先remove

 

当前基本所有的项目都使用了线程池技术，这非常好，可以动态配置线程数、可以重用线程。

 

然而，如果你在项目中使用到了ThreadLocal，一定要记得使用前或者使用后remove一下。这是因为上面提到了线程池技术做的是一个线程重用，这意味着代码运行过程中，一条线程使用完毕，并不会被销毁而是等待下一次的使用。我们看一下Thread类中，持有ThreadLocal.ThreadLocalMap的引用：

 

ThreadLocal.ThreadLocalMap threadLocals = null;

线程不销毁意味着上条线程set的ThreadLocal.ThreadLocalMap中的数据依然存在，那么在下一条线程重用这个Thread的时候，很可能get到的是上条线程set的数据而不是自己想要的内容。

 

这个问题非常隐晦，一旦出现这个原因导致的错误，没有相关经验或者没有扎实的基础非常难发现这个问题，因此在写代码的时候就要注意这一点，这将给你后续减少很多的工作量。

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

 

因为ThreadLocalMap的生命周期和线程是一样长的，不采取这种防范机制，是会造成内存泄漏的。如果多定义了几个ThreadLocal对象，并且线程都将占用内存比较大的对象给放到对应的线程中，可能就会造成OOM异常了。

 

ThreadLocal可能引起的内存泄露：  https://www.cnblogs.com/onlywujun/p/3524675.html

 

threadlocal里面使用了一个存在弱引用的map,当释放掉threadlocal的强引用以后,map里面的value却没有被回收.而这块value永远不会被访问到了. 所以存在着内存泄露. 最好的做法是将调用threadlocal的remove方法.

每个thread中都存在一个map, map的类型是ThreadLocal.ThreadLocalMap. Map中的key为一个threadlocal实例. 这个Map的确使用了弱引用,不过弱引用只是针对key. 每个key都弱引用指向threadlocal. 当把threadlocal实例置为null以后,没有任何强引用指向threadlocal实例,所以threadlocal将会被gc回收. 但是,我们的value却不能回收,因为存在一条从current thread连接过来的强引用. 只有当前thread结束以后, current thread就不会存在栈中,强引用断开, Current Thread, Map, value将全部被GC回收.

 

　　所以得出一个结论就是只要这个线程对象被gc回收，就不会出现内存泄露，但在threadLocal设为null和线程结束这段时间不会被回收的，就发生了我们认为的内存泄露。其实这是一个对概念理解的不一致，也没什么好争论的。最要命的是线程对象不被回收的情况，这就发生了真正意义上的内存泄露。比如使用线程池的时候，线程结束是不会销毁的，会再次使用的。就可能出现内存泄露。　　

 

　　PS.Java为了最小化减少内存泄露的可能性和影响，在ThreadLocal的get,set的时候都会清除线程Map里所有key为null的value。所以最怕的情况就是，threadLocal对象设null了，开始发生“内存泄露”，然后使用线程池，这个线程结束，线程放回线程池中不销毁，这个线程一直不被使用，或者分配使用了又不再调用get,set方法，那么这个期间就会发生真正的内存泄露。

 

=====================================================================================================JSONStr转Map================================================================================================

public static Map<String, String> toMap(final String json)

​    {

​        final Map<String, String> result = new HashMap<String, String>();

​        JSONObject jsonString = null;

​        try

​        {

​            jsonString = new JSONObject(json);

​        }

​        catch (final JSONException e)

​        {

​            LOGGER.error("JsonHelper#toMap new jsonobject parse json error");

​        }

​        if (null == jsonString)

​        {

​            return result;

​        }

 

​        final Iterator iterator = jsonString.keys();     //这一步是关键点

 

​        String value = null;

​        String key = null;

​        while (iterator.hasNext())

​        {

 

​            key = (String)iterator.next();

​            try

​            {

​                value = jsonString.getString(key);

​            }

​            catch (final JSONException e)

​            {

 

​                LOGGER.error("JsonHelper#toMap jsonobject getstring parse json error");

 

​            }

​            result.put(key, value);

 

​        }

​        return result;

​    }

 

=====================================================================================================栈，堆问题================================================================================================

 

​    public void testBookList(){

​        Book bk = new Book();

​        List<Book> bkList = new ArrayList<Book>();

​        for(int j =3; j>0; j--){

​            bk.setBookId("Bookid");

​            bk.setNum(j);

​            bkList.add(bk);

​        }

​        System.out.println(bkList);  

​    }

​    结果：[Book [bookId=Bookid, price=0.0, time=0, num=1], Book [bookId=Bookid, price=0.0, time=0, num=1], Book [bookId=Bookid, price=0.0, time=0, num=1]]

​    

​    遗留的问题：

​    public void testBookList32(){

​        List<Book> bkList = new ArrayList<Book>();

​        for(int j =3; j>0; j--){

​            Book bk = new Book();

​            bk.setNum(j);

​            bkList.add(bk);

​            bk = null;  

​        }

​        System.out.println(bkList);  

​    }

​    结果：[Book [num=3], Book [num=2], Book [num=1]]

​    

=====================================================================================================XML解析================================================================================================

<?xml version="1.0" encoding="UTF-8"?>

<apps>

   <app>

​        <id>id1</id>

​        <key>key1</key>

   </app>

   <app>

​        <id>id2</id>

​        <key>key2</key>

   </app>

</apps>

 

public int writeXML(final AppTemplate templateInfo, String fileName)

​    {

​        fileName = Normalizer.normalize(fileName, Form.NFKC);

​        final Document document = DocumentHelper.createDocument();

​        document.setXMLEncoding(RmtMaintenanceConstants.XML_ENCODING);

​        final Element root = document.addElement("apps");

​        final Element app = root.addElement("app");

​        final Element id = app.addElement("id");

​        final Element key = app.addElement("key");

​        id.addCDATA(templateInfo.getAppId());

​        key.addCDATA(templateInfo.getAppKey());

​        

​        OutputStreamWriter optStreamWriter = null;

​        XMLWriter writer = null;

​        FileOutputStream fileOutputStream = null;

​        try

​        {

​            fileOutputStream = FileUtils.openOutputStream(new File(fileName));

​            optStreamWriter = new OutputStreamWriter(fileOutputStream, RmtMaintenanceConstants.XML_ENCODING);

​            //设置美观的缩进格式，便于阅读

​            final OutputFormat format = OutputFormat.createPrettyPrint();

​            writer = new XMLWriter(System.out, format);

​            writer.setWriter(optStreamWriter);

​            writer.write(document);

​        }

​        catch (final IOException e)

​        {

​            LOG.error("Write xml failed" + e);

​            return RmtMaintenanceConstants.REQUEST_ERROR;

​        }

​        finally

​        {

​            closeStream(optStreamWriter);

​            closeStream(fileOutputStream);

​        }

​        return RmtMaintenanceConstants.REQUEST_SUCCESS;

​    }

​    

public AppTemplate readXML(final String fileName)

​    {

​        final SAXReader reader = new SAXReader();

​        Document doc;

​        try

​        {

​            doc = reader.read(new File(fileName));

​        }

​        catch (final DocumentException e)

​        {

​            LOG.error("Read file exception");

​            return null;

​        }

​        final Element root = doc.getRootElement();

​        final Element bodyElment = root.element("id");

​        final Element titleElement = root.element("key");

​        

​        String body = null;

​        String title = null;

​        if (bodyElment != null)

​        {

​            body = bodyElment.getText();

​        }

​        if (titleElement != null)

​        {

​            title = titleElement.getText();

​        }

​        

​        final AppTemplate templateInfo = new AppTemplate();

​        templateInfo.setAppId(body);

​        templateInfo.setAppKey(title);

​        return templateInfo;

​    }

​    

private void closeStream(final Closeable stream)

   {

​       try

​       {

​           if (null != stream)

​           {

​               stream.close();

​           }

​       }

​       catch (final IOException e)

​       {

​           LOG.error("Close Stream failed");

​       }

   }

   

我:

=====================================================================================================xml对象转xml字符串==================================================================================

import org.jdom.Document;

import org.jdom.Element;

import org.jdom.input.SAXBuilder;

import org.jdom.output.Format;

import org.jdom.output.XMLOutputter;

 

public static String getRequestXml(IReportType reportType, Element content)

​        throws OMSException

​    {

​        Element auth = getRequestAuth(reportType);

​        

​        String xmlStr = null;

​        Element root = new Element("MESSAGE");

​        Document doc = new Document(root);

​        root.addContent(auth);

​        root.addContent(content);

​        XMLOutputter outp = new XMLOutputter();

​        Format format = Format.getPrettyFormat();

​        format.setEncoding(OmuConstants.DECODE_TYPE);

​        outp.setFormat(format);

​        xmlStr = outp.outputString(doc);

​        return xmlStr;

​    }

​    

public static Document string2Doc(String xmlStr)

​        throws OMSException

​    {

​        if (StringUtils.isBlank(xmlStr))

​        {

​            LOGGER.error("xmlStr is empty.");

​            throw new OMSException(ErrorCode.UCC_IVS_PARSE_RESPONSE_ERROR, "");

​        }

​        xmlStr = xmlStr.replaceAll("&", "&amp;");

​        xmlStr = xmlStr.replaceAll("xml", "x");

​        try

​        {

​            java.io.Reader in = new StringReader(xmlStr);

​            SAXBuilder sb = new SAXBuilder();

​            sb.setFeature("http://apache.org/xml/features/disallow-doctype-decl", true);

​            

​            sb.setEntityResolver(new EntityResolver()

​            {

​                String emptyDtd = "";

​                

​                ByteArrayInputStream bytels = new ByteArrayInputStream(emptyDtd.getBytes("UTF-8"));

​                

​                /**

​                 \* {@inheritDoc}

​                 */

​                @Override

​                public InputSource resolveEntity(String publicId, String systemId)

​                    throws SAXException, IOException

​                {

​                    return new InputSource(bytels);

​                }

​            });

​            

​            Document doc = sb.build(in);

​            return doc;

​        }

​        catch (Exception e)

​        {

​            LOGGER.error("string2Doc Exception.e", e);

​            throw new OMSException(ErrorCode.UCC_IVS_PARSE_RESPONSE_ERROR, "", e);

​        }

​    }

 

 

 

=====================================================================================================文件下载================================================================================================

 

public void returnFile(final HttpServletRequest request, final HttpServletResponse response, final String path)

​    {

​        // path是指欲下载的文件的路径。

​        final File file = new File(path);

​        if (!file.exists())

​        {

​            LOG.error("Path {} file not exists.", path);

​            return;

​        }

​        String filename = file.getName();

​        try

​        {

​            // 中文文件名乱码问题

​            final String agent = request.getHeader("User-Agent");

​            if (agent.toUpperCase(Locale.US).indexOf("MSIE") != -1)

​            { // 针对IE或IE内核的浏览器

​                filename = URLEncoder.encode(filename, "UTF-8");

​            }

​            else

​            { // 非IE浏览器的处理

​                filename = new String(filename.getBytes("UTF-8"), "ISO8859-1");

​            }

​        }

​        catch (final UnsupportedEncodingException e)

​        {

​            LOG.error("download is failed");

​            return;

​        }

​        

​        response.reset();

​        response.setContentType("application/x-download;charset=utf-8");

​        response.addHeader("Content-Disposition", String.format("attachment;filename=\"%s\"", filename));

​        response.setCharacterEncoding("UTF-8");

​        OutputStream toClient = null;

​        try

​        {

​            // 以流的形式下载文件。

​            toClient = new BufferedOutputStream(response.getOutputStream());

​            toClient.write(getBuffer(path));

​            toClient.flush();

​        }

​        catch (final IOException e)

​        {

​            LOG.error("download is failed");

​            return;

​        }

​        finally

​        {

​            FileUtil.closeQuietly(toClient);

​        }

​    }

​    

​    private byte[] getBuffer(final String path)

​    {

​        byte[] buffer = new byte[0];

​        InputStream fis = null;

​        FileInputStream fileInputStream = null;

​        try

​        {

​            fileInputStream = new FileInputStream(path);

​            fis = new BufferedInputStream(fileInputStream);

​            buffer = new byte[fis.available()];

​            final int res = fis.read(buffer);

​            if (res < 0)

​            {

​                LOG.info("the stream is at the end of the file");

​            }

​        }

​        catch (final IOException e)

​        {

​            LOG.error("download is failed");

​        }

​        finally

​        {

​            closeStream(fis);

​            closeStream(fileInputStream);

​        }

​        return buffer;

​    }

​    

​    /**

​     \* 关闭IO流

​     \* @param stream 要关闭的流

​     */

​    private void closeStream(final Closeable stream)

​    {

​        try

​        {

​            if (null != stream)

​            {

​                stream.close();

​            }

​        }

​        catch (final IOException e)

​        {

​            LOG.error("Close Stream failed");

​        }

​    }

我:

=====================================================================================================字符转换================================================================================================

​    function strReplace(str) {

​        var newStr = str.replace(/</g, "&lt;").replace(/>/g, "&gt;").replace(/"/g, "&quot;").replace(/ /g, "&nbsp;");

​        return newStr;

​    }

 

function(string) {

​            if (!string) {

​                return string

​            }

​            var unescapers = {"&amp;": "&","&lt;": "<","&gt;": ">","&quot;": '"',"&#x27;": "'","&#x28;": "(","&#x29;": ")","&copy;": "\xa9"}, unescaper = /(&amp;|&lt;|&gt;|&quot;|&#x27;|&#x28;|&#x29;|&copy;)/g, tmpStr = "";

​            return (tmpStr + string).replace(unescaper, function(match) {

​                return unescapers[match]

​            })

​        }

 

=====================================================================================================导出文件到excel================================================================================================

public class ExportRecordMgr

{

​    /**

​     \* 根路径

​     */

​    public static final String ROOT_PATH = new StringBuffer().append(System.getProperty("oms.path.var"))

​        .append(File.separator)

​        .append("storage")

​        .append(File.separator)

​        .append("enterprise.app.rmtmaintenancere")

​        .toString();

​        

​    /**

​     \* 导出excel列名

​     */

​    private static final String[] CMD_COLUMN_TITLES = {WebTelnetConstants.SHEET_NAME_TIME,

​        WebTelnetConstants.SHEET_NAME_COMMAND};

​        

​        

​    private String createExcel(String path, final RmtTaskInfo taskInfo, final List<List<CmdRecordInfo>> cmdRecord)

​    {

​        WritableWorkbook book = null;

​        try

​        {

​            path = Normalizer.normalize(path, Form.NFKC);

​            final File file = new File(path);

 

​            final WorkbookSettings workbookSettings = new WorkbookSettings();

​            workbookSettings.setGCDisabled(true);

​            // 开始创建文件

​            book = Workbook.createWorkbook(file, workbookSettings);

​            boolean emptySheet = true;

​            int delIndex = 1;

​            for (int i = 0; i < cmdRecord.size(); i++)

​            {

​                final List<CmdRecordInfo> records = cmdRecord.get(i);

​                if (records.size() < 1)

​                {

​                    continue;

​                }

​                emptySheet = false;

​                String sheetName = getNeName(records.get(0).getNeId(), taskInfo);

​                if (sheetName.equals(WebTelnetConstants.FILE_DELETED_NAME))

​                {

​                    sheetName += delIndex++;

​                }

​                final WritableSheet sheet = book.createSheet(sheetName, i);

​                createSheet(sheet, records);

​            }

​            if (emptySheet)

​            {

​                createTitle(book.createSheet("Sheet", 0));

​                LOG.info("Has empty records.");

​            }

​            book.write();

​        }

​        catch (final IOException e)

​        {

​            LOG.error("cannot create excel.");

​        }

​        finally

​        {

​            if (null != book)

​            {

​                try

​                {

​                    book.close();

​                }

​                catch (final WriteException e)

​                {

​                    LOG.error("WriteException");

​                }

​                catch (final IOException e)

​                {

​                    LOG.error("IOException");

​                }

​            }

​        }

​        return path;

​    }

​    

​    /**

​     \* 创建sheet

​     *

​     \* @param sheet

​     \* @param records

​     */

​    private void createSheet(final WritableSheet sheet, final List<CmdRecordInfo> records)

​    {

​        createTitle(sheet);

​        int rowIndex = 1;

​        for (final CmdRecordInfo record : records)

​        {

​            createContent(sheet, rowIndex, record);

​            rowIndex++;

​        }

​    }

​    

​    

​    /**

​     \* 创建sheet的内容

​     *

​     \* @param sheet

​     \* @param row

​     \* @param record

​     */

​    private void createContent(final WritableSheet sheet, final int row, final CmdRecordInfo record)

​    {

​        try

​        {

​            int i = 0;

​            sheet.addCell(new Label(i++, row, DateTransferUtil.longToString(record.getExetime())));

​            sheet.addCell(new Label(i++, row, record.getCmdStr()));

​        }

​        catch (final RowsExceededException e)

​        {

​            LOG.error("RowsExceededException create Content failed {}", e.getMessage());

​        }

​        catch (final WriteException e)

​        {

​            LOG.error("WriteException create Content failed {}", e.getMessage());

​        }

​    }

​    

​    /**

​     \* 创建sheet的标题

​     *

​     \* @param sheet 表格

​     */

​    private void createTitle(final WritableSheet sheet)

​    {

​        try

​        {

​            int i = 0;

​            for (final String field : CMD_COLUMN_TITLES)

​            {

​                final Label label = new Label(i++, 0, field);

​                sheet.addCell(label);

​            }

​        }

​        catch (final RowsExceededException e)

​        {

​            LOG.error("RowsExceededException create title failed {}", e.getMessage());

​        }

​        catch (final WriteException e)

​        {

​            LOG.error("WriteException create title failed {}", e.getMessage());

​        }

​    }

​    

​    /**

​     \* mkDir

​     *

​     \* @param path path

​     */

​    private void mkDir(String path)

​    {

​        path = Normalizer.normalize(path, Form.NFKC);

​        final File tempFile = new File(path);

​        if (!tempFile.exists())

​        {

​            if (!tempFile.mkdirs())

​            {

​                LOG.warn("Warning!!!!! Failed creating temp directory!");

​                return;

​            }

​        }

​    }

我:

=====================================================================================================压缩================================================================================================

/**

​     \* 将存放在sourceFilePath目录下的源文件，

​     \* 打包成fileName名称的zip文件，并存放到源路径下

​     *

​     \* @param sourceFilePath 待压缩的文件路径

​     \* @param fileName       压缩后文件的名称

​     \* @return 压缩后的文件路径

​     */

​    private String fileToZip(String sourceFilePath, final String fileName)

​    {

​        sourceFilePath = Normalizer.normalize(sourceFilePath, Form.NFKC);

​        final File sourceFile = new File(sourceFilePath);

​        if (!sourceFile.exists())

​        {

​            if (!sourceFile.mkdirs())

​            {

​                LOG.error("mkdirs error.");

​                return "";

​            }

​        }

​        String filePath =

​            new StringBuffer().append(ROOT_PATH)

​                .append(File.separator)

​                .append(fileName)

​                .append(getTime())

​                .append(".zip")

​                .toString();

​        filePath = Normalizer.normalize(filePath, Form.NFKC);

​        FileOutputStream outputStream;

​        ZipOutputStream out;

​        try

​        {

​            outputStream = FileUtils.openOutputStream(new File(filePath));

​            out = new ZipOutputStream(new BufferedOutputStream(outputStream));

​            out.setEncoding("GBK");

​            createCompressedFile(out, sourceFile, "");

​            out.close();

​        }

​        catch (final FileNotFoundException e)

​        {

​            LOG.error("FileNotFoundException: {}", e.getMessage());

​            return null;

​        }

​        catch (final IOException e)

​        {

​            LOG.error("FileOutputStream close failed.");

​            return null;

​        }

 

​        return filePath;

​    }

​    

​    

​    /**

​     \* 生成压缩文件。

​     \* 如果是文件夹，则使用递归，进行文件遍历、压缩

​     \* 如果是文件，直接压缩

​     *

​     \* @param out  输出流

​     \* @param file 文件

​     \* @param dir  目录

​     \* @throws Exception

​     */

​    private void createCompressedFile(final ZipOutputStream out, final File file, String dir)

​    {

​        //文件输入流

​        FileInputStream fis = null;

​        try

​        {

​            //如果当前的是文件夹，则进行进一步处理

​            if (file.isDirectory())

​            {

​                //得到文件列表信息

​                final File[] files = file.listFiles();

​                //将文件夹添加到下一级打包目录

​                if (files == null)

​                {

​                    LOG.error("File is null");

​                    return;

​                }

​                out.putNextEntry(new ZipEntry(dir + File.separator));

 

​                dir = dir.length() == 0 ? "" : dir + File.separator;

 

​                //循环将文件夹中的文件打包

​                for (final File file2 : files)

​                {

​                    createCompressedFile(out, file2, dir + file2.getName());

​                }

​            }

​            else

​            {

​                //当前的是文件，打包处理

​                fis = new FileInputStream(file);

 

​                out.putNextEntry(new ZipEntry(dir));

​                //进行写操作

​                int read = 0;

​                final byte[] buffer = new byte[1024];

​                while ((read = fis.read(buffer)) > 0)

​                {

​                    out.write(buffer, 0, read);

​                }

​            }

​        }

​        catch (final IOException e)

​        {

​            LOG.error("compress file error.");

​        }

​        finally

​        {

​            if (fis != null)

​            {

​                //关闭输入流

​                try

​                {

​                    fis.close();

​                }

​                catch (final IOException e)

​                {

​                    LOG.error("close fileInputStream failed.");

​                }

​            }

​        }

​    }

 

=====================================================================================================ROAResult================================================================================================

/**

\* ROA的返回结果 {resut:"success",data:{"name" : "cxxx"}}

*

\* @author l00338041

*/

public class ROAResult

{

​    /**

​     \* 常量失败

​     */

​    public static final String FAILED = "failed";

 

​    /**

​     \* 常量成功

​     */

​    public static final String SUCCESSED = "successed";

 

​    private String result;

 

​    private String failedReason;

 

​    private Object data;

 

​    private String errorCode;

 

​    private boolean ifIsViewOnly = false;

 

​    /**

​     \* 构造函数

​     *

​     \* @param result       result 结果

​     \* @param failedReason failedReason 错误原因

​     */

​    private ROAResult(final String result, final String failedReason)

​    {

​        this.result = result;

​        this.failedReason = failedReason;

​    }

 

​    /**

​     \* 构造函数

​     *

​     \* @param result result 结果

​     \* @param data   data 返回的数据对象

​     */

​    public ROAResult(final String result, final Object data)

​    {

​        this.result = result;

​        this.data = data;

​    }

 

​    /**

​     \* 获取一个失败时的对象

​     *

​     \* @param failedReason 失败原因

​     \* @return ROAResult

​     */

​    public static ROAResult newFailure(final String failedReason)

​    {

​        return new ROAResult(FAILED, failedReason);

​    }

 

​    /**

​     \* 获取一个失败时的对象

​     *

​     \* @param failedReason 失败原因

​     \* @param errorCode    错误码

​     \* @return ROAResult

​     */

​    public static ROAResult newFailure(final String failedReason, final String errorCode)

​    {

​        final ROAResult ros = new ROAResult(FAILED, failedReason);

​        ros.setErrorCode(errorCode);

​        return ros;

​    }

 

​    /**

​     \* 获取一个成功时的对象

​     *

​     \* @param data 数据

​     \* @return ROAResult

​     */

​    public static ROAResult newSuccess(final Object data)

​    {

​        return new ROAResult(SUCCESSED, data);

​    }

}    

 

我:

=====================================================================================================解析Property文件================================================================================================

​            fileInputStream = new FileInputStream(ntcCigFile);

​            pro = new Properties();

​            pro.load(fileInputStream);

​            pro.get(ESIGHT_SERVER_IP)；

 

 

=====================================================================================================enum================================================================================================

public enum ConstrainType implements Serializable

{

​    equal, greater, smaller, like, notEqual, notGreater, notSmaller, notLike, and, or, in, notIn;

}

 

final ConstrainType constrainType = operMap.get(field);

 

​    private void constraint(final ConstrainType constrainType, final Constraint constraint)

​    {

​        switch (constrainType)

​        {

​            case greater:

​                constraint.greater();

​                break;

​            case in:

​                constraint.in();

​                break;

​        }

​    }

 

=====================================================================================================自定义线程工厂类================================================================================================

/**

*

\* NAS专用线程池工厂类。给线程加上标记，以与其他模块区分开

\* @author  w00223541

\* @version  [eSight V3R6, 2016-3-23]

*/

public final class NameServiceThreadFactory implements ThreadFactory

{

​    /** 线程前缀 */

​    private static final String NAMEPREFIX = "nas-nameservice-pool-thread-";

​    

​    /** 线程当前编号 */

​    private final AtomicInteger threadNumber = new AtomicInteger(1);

​    

​    /** 线程组。获取线程组的代码，沿袭DefaultThreadFactory */

​    private final ThreadGroup group;

​    

​    private final String customNamePrefix;

​    

​    private boolean isDaemonThread = false;

​    

​    /**

​     \* 构造函数

​     \* @param namePrefix 自定义前缀

​     \* @param isDaemon 是否是守护线程

​     */

​    public NameServiceThreadFactory(final String namePrefix, final boolean isDaemon)

​    {

​        final SecurityManager security = System.getSecurityManager();

​        isDaemonThread = isDaemon;

​        customNamePrefix = namePrefix;

​        group = security != null ? security.getThreadGroup() : Thread.currentThread().getThreadGroup();

​    }

​    

​    /**

​     \* {@inheritDoc}

​     */

​    @Override

​    public Thread newThread(final Runnable runnable)

​    {

​        String threadName = NAMEPREFIX;

​        if (StringUtils.isEmpty(customNamePrefix))

​        {

​            threadName += threadNumber.getAndIncrement();

​        }

​        else

​        {

​            threadName += customNamePrefix + "-" + threadNumber.getAndIncrement();

​        }

​        

​        final Thread thread = new Thread(group, runnable, threadName);

​        thread.setDaemon(isDaemonThread);

​        

​        return thread;

​    }

​    

}

 

 

public class IvsCommonThreadFactory implements ThreadFactory

{

​    private final AtomicLong threadCounter;

​    

​    private final ThreadFactory wrappedFactory;

​    

​    private final String namingPattern;

​    

​    /**

​     \* 创建线程池工厂，对线程进行命名

​     *

​     \* @param namePattern

​     \*            线程名的正则表达式：myThread_clean_file-%d

​     */

​    public IvsCommonThreadFactory(String namePattern)

​    {

​        wrappedFactory = Executors.defaultThreadFactory();

​        namingPattern = namePattern;

​        threadCounter = new AtomicLong();

​    }

​    

​    /**

​     \* {@inheritDoc}

​     */

​    @Override

​    public Thread newThread(final Runnable r)

​    {

​        final Thread t = this.wrappedFactory.newThread(r);

​        initializeThread(t);

​        return t;

​    }

​    

​    private void initializeThread(final Thread t)

​    {

​        if (this.namingPattern != null)

​        {

​            final Long count = Long.valueOf(threadCounter.incrementAndGet());

​            t.setName(String.format(this.namingPattern, count));

​        }

​    }

}

 

=====================================================================================================JSONUtil================================================================================================

public abstract class JSONUtil

{

​    /**

​     \* 日志

​     */

​    private static final Logger LOGGER = OMSLogFactory.getLog(JSONUtil.class);

​    

​    /**

​     \* 对象转换成String <一句话功能简述> <功能详细描述>

​     *

​     \* @param t 对象

​     \* @return String

​     \* @see [类、类#方法、类#成员]

​     */

​    public static String objectToString(Object t)

​    {

​        ObjectMapper mapper = new ObjectMapper();

​        String json = "";

​        try

​        {

​            json = mapper.writeValueAsString(t);

​        }

​        catch (JsonGenerationException e)

​        {

​            LOGGER.error("exception is:", e);

​        }

​        catch (JsonMappingException e)

​        {

​            LOGGER.error("exception is:", e);

​        }

​        catch (IOException e)

​        {

​            LOGGER.error("IOException");

​        }

​        return json;

​    }

​    

​    /**

​     \* String转成对象 <一句话功能简述> <功能详细描述>

​     *

​     \* @param <T> 泛型

​     \* @param string 字符串

​     \* @param class1 对象

​     \* @return javabean 转成的对象

​     */

​    public static <T> T stringToObject(String string, final Class<T> class1)

​    {

​        ObjectMapper mapper = new ObjectMapper();

​        T result = null;

​        try

​        {

​            result = mapper.readValue(string, class1);

​        }

​        catch (JsonParseException e)

​        {

​            LOGGER.error("exception is:", e);

​        }

​        catch (JsonMappingException e)

​        {

​            LOGGER.error("exception is:", e);

​        }

​        catch (IOException e)

​        {

​            LOGGER.error("IOException");

​        }

​        return result;

​    }

​    

​    /**

​     \* String转成对象

​     *

​     \* @param string 字符串

​     \* @param class1 对象

​     \* @param <T> 泛型

​     \* @return 转成的对象

​     \* @throws OMSException 参数异常

​     */

​    public static <T> T strToObj(String string, final Class<T> class1)

​        throws OMSException

​    {

​        ObjectMapper mapper = new ObjectMapper();

​        T result = null;

​        try

​        {

​            result = mapper.readValue(string, class1);

​        }

​        catch (JsonParseException e)

​        {

​            LOGGER.error("exception is:", e);

​            throw new OMSException("exception is:", e);

​        }

​        catch (JsonMappingException e)

​        {

​            LOGGER.error("exception is:", e);

​            throw new OMSException("exception is:", e);

​        }

​        catch (IOException e)

​        {

​            LOGGER.error("IOException");

​            throw new OMSException("IOException", e);

​        }

​        return result;

​    }

}

 

=====================================================================================================单例模式的Spring配置================================================================================================

  <bean name="restUtil"

​        class="[enterprise.app.nas.manager.as.communication.RestUtil](http://enterprise.app.nas.manager.as.communication.restutil/)"

​        factory-method="getInstance">

 

​    

=====================================================================================================从reader中读取一行================================================================================================

 

public static String readOneLine(final BufferedReader reader)

​        throws IOException

​    {

​        final StringBuffer sb = new StringBuffer();

​        int intC;

​        while ((intC = reader.read()) != -1)

​        {

​            final char c = (char)intC;

​            if (c == '\n' || c == '\r')

​            {

​                return sb.toString();

​            }

​            if (sb.length() >= MAX_STR_LEN)

​            {

​                throw new IOException("input too long");

​            }

​            sb.append(c);

​        }

​        if (sb.length() > 0)

​        {

​            return sb.toString();

​        }

​        return null;

​    }

​    

=====================================================================================================服务器端解析特殊字符================================================================================================    

public static String validCustomTitle(final String customTitle)

​    {

​        if (customTitle == null)

​        {

​            return "";

​        }

​        String normalizedString = Normalizer.normalize(customTitle, Form.NFKC);

​        normalizedString = replaceString(normalizedString, "&amp;", "&");

​        normalizedString = replaceString(normalizedString, "&lt;", "<");

​        normalizedString = replaceString(normalizedString, "&gt;", ">");

​        normalizedString = replaceString(normalizedString, "&apos;", "'");

​        normalizedString = replaceString(normalizedString, "&quot;", "\"");

​        normalizedString = replaceString(normalizedString, "&#40;", "(");

​        normalizedString = replaceString(normalizedString, "&#41;", ")");

​        

​        return normalizedString;

​    }

​    

private static String replaceString(String strData, final String regex, final String replacement)

​    {

​        if (strData == null)

​        {

​            return null;

​        }

​        int index;

​        index = strData.indexOf(regex);

​        final StringBuffer strNew = new StringBuffer();

​        if (index >= 0)

​        {

​            while (index >= 0)

​            {

​                strNew.append(strData.substring(0, index)).append(replacement);

​                strData = strData.substring(index + regex.length());

​                index = strData.indexOf(regex);

​            }

​            strNew.append(strData);

​            return strNew.toString();

​        }

​        return strData;

​    }

​    

​    

我:

=====================================================================================================Mgr层所传的类型与返回的类型可以一样===========================================================================================    

​    

public class ClusterMgrBean

{

​    /**

​     \* 集合的列过滤条件

​     */

​    private ClusterFilterBean clusterFilter;

​    

​    /**

​     \* 起始页

​     */

​    private int pageBegin;

​    

​    /**

​     \* 每页显示条目数

​     */

​    private int pageLength;

​    

​    /**

​     \* 当前页

​     */

​    private int currentPage;

​    

​    //集群列排序

​    private String columnName;

​    

​    private String columnSort;

​    

​    

​    //以下为返回的值

​    

​    /**

​     \* 集群列表数据

​     */

​    private List<ClusterDO> clusterList;

​    

​    /**

​     \* VCN列表数据

​     */

​    private List<VcnDO> vcnList;

​    

​    /**

​     \* 总数. totalRecord

​     */

​    private int totalRecord;

}    

​    

​    MGR:

​     public ClusterMgrBean queryAllCustomerInfo(final ClusterMgrBean mgrDO)

​    {

 

​        final ClusterFilterBean filterVO = mgrDO.getClusterFilter();

 

​        int totalCount = 0;

 

​        final IHostEIPCfgDao hostEIPCfgDao = getHostEIPCfgDao();

​        if (null == hostEIPCfgDao)

​        {

​            return mgrDO;   //直接返回mgrDO，则 clusterList、vcnList 都为 NULL

​        }

​    }

​    

 

=====================================================================================================程序启动时运行XX================================================================================================

<bean id="ivsStopDetect" class="com.huawei.oms.esight.ucc.ivs.ipca.timer.StopDetectTimer"

​        init-method="start" destroy-method="stop">

</bean>

 

Spring提供的init-method的功能来执行一个bean 子定义的初始化方法,这可以在一个bean的配置文件中通过init-method声明:

init-method指定的方法可以是public、protected以及private的，并且方法也可以是final的。

init-method指定的方法可以是声明为抛出异常的，如果在init-method方法中抛出了异常，

那么Spring将中止这个Bean的后续处理，并且抛出一个org.springframework.beans.factory.BeanCreationException异常。

 

在spring中通过配置init-method和destroy-method方法来实现Bean的初始化和销毁时附加的操作。

 

比如初始化一个对象（bean）后立即初始化（加载）一些数据，在销毁一个对象之前进行垃圾回收等等。

根据打印顺序可以看到，首先是构造函数，也就是创建了bean，紧接着执行了init，然后再context.close要销毁bean之前又执行了destroy。

 

 

public class Test3 {

​    public void init() {

​        System.out.println("this is init method3");

​    }

​    public Test3() {

​        super();

​        System.out.println("构造函数3");

​    }

​    public void destroy() {

​        System.out.println("this is destroy method3");

​    }

​    public void test() {

​        System.out.println("testttttttt");

​    }

}

 

<bean id="initOrDestroyTest" class="springTest2.Test3" init-method="init" destroy-method="destroy">

</bean>

 

public static void main(String[] args) {

​        ClassPathXmlApplicationContext context1 = new ClassPathXmlApplicationContext("spring.xml");

​        System.out.println("#################################");

​        context1.close();

}

结果：

构造函数3

this is init method3    

\#################################

this is destroy method3

 

 

 

 

init-method是在构造函数之后执行，而静态代码块的初始化是在构造函数之前执行，(静态代码块 是属于类，init-method是属于类的对象)非静态代码块的初始化是在构造函数之时执行

静态代码块    ： static{}

非静态代码块  ： {}

 

 

小总结：

类的加载：

什么叫类的加载  ：虚拟机通过流从磁盘上把class文件读入到虚拟机中的过程

什么时候类的加载：分为饿汉式加载和懒汉式加载，饿汉式加载：只要有其他类引用了它就加载，懒汉式加载：反射，等到类的初始化时才加载。

类的加载完成后会有一个准备的阶段：为类的静态变量分配内存并将其初始化为默认值，准备阶段不分配类中实例变量的内存。

以上准备完成后：

定义main方法的那个类先初始化。

类的初始化也叫类的静态域初始化。

当创建类的实例的时候：会执行类的初始化，初始化分为：也叫：类的静态域初始化、而非静态域初始化在类的构造函数执行之前，静态域初始化在非静态域初始化之前，初始化在类的构造函数之前完成。init-method在类的构造函数之后完成

当调用类的静态变量、静态方法时 会执行类的静态域初始化，调用类的静态常量时不会触发初始化

当初始化一个类的时候，会先初始化其父类，对于静态字段的访问，只有直接定义这个字段的类才会初始化。

 

类的静态域初始化：

为类的静态变量赋值 并 执行static{}块，顺序是从上而下顺序执行。

类的非静态域初始化：

执行{}中代码。

无论类被初始化几次，静态域初始化只会在第一次执行，非静态域初始化会在每次创建实例之前执行，init-method会在构造函数之后执行

 

public class A {

​    {

​        System.out.println("A---222");

​    }

​    static{

​        System.out.println("A---111");

​    }

 

​    public A(){

​        System.out.println("A---333");

​    }

}

public class B {

​    {

​        System.out.println("B---222");

​    }

​    static{

​        System.out.println("B---111");

​    }

​    public B(){

​        System.out.println("B---333");

​    }

​    public static void main(String[] args) {

​        A a = new A();

​    }

}

结果：

B---111    //定义main 的方法先初始化，初始化只初始化类的静态域。

A---111    //静态域初始化在非静态域初始化之前，非静态域初始化只在类的实例创建期间执行，也即构造函数执行之前

A---222

A---333

 

 

来个骚一点的：

public class A {

​    {

​        System.out.println("A---222");

​    }

​    static{

​        System.out.println("A---111");

​    }

 

​    public A(){

​        System.out.println("A---333");

​    }

}

public class B {

​    {

​        System.out.println("B---222");

​    }

​    private static A a2 = new A();

​    static{

​        System.out.println("B---111");

​    }

​    public B(){

​        System.out.println("B---333");

​    }

​    public static void main(String[] args) {

​        System.out.println("B---444");

​        A a = new A();

​        System.out.println("B---555");

​    }

}

 

定义main的类先初始化：B先初始化，也即静态域初始化：执行static{}代码块，为静态变量赋值，从上到下依次执行。

a2准备阶段是null，为其赋值a2 = new A(); 创建A的实例了，创建实例之前，又要先初始化A：

System.out.println("A---111");

调用构造函数了，再调用之前，先执行非静态域初始化：

System.out.println("A---222");

System.out.println("A---333");

A初始化好了，继续向下执行，一个类只会加载一次：

System.out.println("B---111");

执行main：

System.out.println("B---444");

A a = new A(); A要初始化，静态域初始化只会在第一次执行，非静态域初始化会在每次创建实例之前执行

System.out.println("A---222");

System.out.println("A---333");

然后：

System.out.println("B---555");

 

结果：

A---111

A---222

A---333

B---111

B---444

A---222

A---333

B---555

 

也即：

​    static{

​        System.out.println("A---111");

​    }

​    与类有关

​    

​    {

​        System.out.println("A---222");

​    }

​    与类的实例有关，只要创建了类的实例就会执行这个代码块

​    

 

​    

​    

public class B {

​    {

​        System.out.println("B---222");

​    }

​    static{

​        System.out.println("B---111");

​    }

​    private static A a2 = new A();

​    public B(){

​        System.out.println("B---333");

​    }

​    public static void main(String[] args) {

​        System.out.println("B---444");

​        A a = new A();

​        System.out.println("B---555");

​    }

}

结果：

B---111

A---111

A---222

A---333

B---444

A---222

A---333

B---555

 

 

小结：

初始化类，与初始化类的实例，

初始化类： 为类的静态变量赋值 和 执行类的静态代码块，从上而下一次执行。

初始化类的实例： 先执行{}代码块，再执行类的构造函数，在执行init-method

init-method：比如初始化一个对象（bean）后立即初始化（加载）一些数据，是附加操作，destory-method：在销毁一个对象之前进行垃圾回收等等。

 

类的实例都要创建了，这个类肯定要先初始化。所以说类的构造函数里不写与业务相关的逻辑，放到init-method 里。

 

new一个对象的时候，初始化顺序是，父类静态>子类静态>父类属性>父类构造器>子类属性>子类构造器

 

 

 

 

 

 

 

 

=====================================================================================================服务器端解析特殊字符================================================================================================    

 

Map<String, MoOfflineInfo> moOfflineMap = Collections.synchronizedMap(new HashMap<String, MoOfflineInfo>());

 

 

​            <[and upper(APNAME) like '%'||upper(:APNAME)||'%' ESCAPE '\']>

​            

​            <[ order by <%:orderStatus%> nlssort(<%:orderColumn%>,'NLS_SORT=SCHINESE_PINYIN_M') <%:orderType%>]>

 

=====================================================================================================REST服务后台接受参数，要先对param进行解码==========================================================================

​        // 解码

​        param = IempHtmlUtils.htmlUnescape(param);

​        condition = JSONUtil.strToObj(param, InterfaceCon.class);

​        

​        String[][] BASIC_ESCAPE = { {"&", "&amp;"}, {"<", "&lt;"}, {">", "&gt;"}, {"\"", "&quot;"},

​        {"'", "&#x27;"}, {"", "&copy;"}, {"(", "&#x28;"}, {")", "&#x29;"}};

 

=====================================================================================================后台校验==========================================================================

 

​        //服务器端参数校验

​        int neIpLength = condition.getDeviceQueryCon().getNeIp() == null ? 0 : condition.getDeviceQueryCon().getNeIp().length();

​        int aliasNameLength = condition.getDeviceQueryCon().getAliasName() == null ? 0 : condition.getDeviceQueryCon().getAliasName().length();

​        if(neIpLength>15 || aliasNameLength>250)

​        {

​            SMUtil.getInstance().kickOffUser();

​            roaResult.setResultCode(ConfigConstants.NO_PERMIT);

​            return roaResult;

​        }

 

 

=====================================================================================================Enum==========================================================================

public enum TrafficeTypeEnum

{

​    /**

​     \* 字节

​     */

​    Byte(0),

 

​    /**

​     \* 包

​     */

​    Packet(1);

​    

​    /**

​     \* 类型值

​     */

​    private final int value;

​    

​    /**

​     \* 构造函数

​     \* @param value 类型值

​     */

​    private TrafficeTypeEnum(final int value)

​    {

​        this.value = value;

​    }

​    

​    public int getValue()

​    {

​        return value;

​    }

​    

​    /**

​     \* 通过流量类型值获取流量类型枚举

​     \* @param value 流量类型值

​     \* @return 返回流量类型枚举

​     */

​    public static TrafficeTypeEnum getEnum(final int value)

​    {

​        for (TrafficeTypeEnum trafficeTypeEnum : TrafficeTypeEnum.values())

​        {

​            if (trafficeTypeEnum.getValue() == value)

​            {

​                return trafficeTypeEnum;

​            }

​        }

​        return null;

​    }

}

 

public enum AlarmLevelEnum

{

​    /**

​     \* 紧急

​     */

​    Critical(1, 2),

 

​    /**

​     \* 重要

​     */

​    Major(2, 1.5),

 

​    /**

​     \* 次要

​     */

​    Minor(3, 1.2),

​    /**

​     \* 提示

​     */

​    Warning(4, 1.05);

​    

​    /**

​     \* 告警级别值

​     */

​    private final int value;

​    

​    private final double defaultValueRate;

​    

​    /**

​     \* 构造函数

​     \* @param value 类型值

​     */

​    private AlarmLevelEnum(final int value, final double defaultValueRate)

​    {

​        this.value = value;

​        this.defaultValueRate = defaultValueRate;

​    }

​    

​    public int getValue()

​    {

​        return value;

​    }

​    

​    public double getDefaultValueRate()

​    {

​        return defaultValueRate;

​    }

​    

​    /**

​     \* 通过告警级别值获取告警级别枚举

​     \* @param value 告警级别值

​     \* @return 返回告警级别枚举

​     */

​    public static AlarmLevelEnum getEnum(final int value)

​    {

​        for (AlarmLevelEnum alarmLevelEnum : AlarmLevelEnum.values())

​        {

​            if (alarmLevelEnum.getValue() == value)

​            {

​                return alarmLevelEnum;

​            }

​        }

​        return null;

​    }

}

我:

=====================================================================================================Enum===================================================================================================

​    /**

​     \* 替换字符串中的特殊字符

​     \* @param str 含有特殊字符的字符串

​     \* @return 替换后的字符

​     */

​    public static String replaceValidString(final String str)

​    {

​        if (str == null)

​        {

​            return "";

​        }

​        String normalizedString = Normalizer.normalize(str, Form.NFKC);

​        normalizedString = replaceString(normalizedString, "&", "&amp");

​        normalizedString = replaceString(normalizedString, "<", "&lt");

​        normalizedString = replaceString(normalizedString, ">", "&gt");

​        normalizedString = replaceString(normalizedString, "'", "&apos");

​        normalizedString = replaceString(normalizedString, "\"", "&quot");

​        normalizedString = replaceString(normalizedString, "(", "&#40");

​        normalizedString = replaceString(normalizedString, ")", "&#41");

​        

​        return normalizedString;

​    }

​    

​    private static String replaceString(String strData, final String regex, final String replacement)

​    {

​        if (strData == null)

​        {

​            return null;

​        }

​        int index;

​        index = strData.indexOf(regex);

​        final StringBuffer strNew = new StringBuffer();

​        if (index >= 0)

​        {

​            while (index >= 0)

​            {

​                strNew.append(strData.substring(0, index)).append(replacement);

​                strData = strData.substring(index + regex.length());

​                index = strData.indexOf(regex);

​            }

​            strNew.append(strData);

​            return strNew.toString();

​        }

​        return strData;

​    }

 

=====================================================================================================后台校验===================================================================================================

 

/**

​     \* 是否非空，并且不包含"#%&'+/;<=>?\

​     \* @param str 待校验字符串

​     \* @return 正确返回true，错误返回false

​     */

​    public boolean noSpecialSymbol(String str)

​    {

​        if (null != str && !str.isEmpty())

​        {

​            //归一化

​            str = Normalizer.normalize(str, Form.NFKC);

​            //正则表达式

​            final String regex = "^[^\"#%&\'+/;<=>?\\\\]*$";

​            if (str.matches(regex))

​            {

​                return true;

​            }

​        }

​        return false;

​    }

 

=====================================================================================================enum===================================================================================================

public enum FTPType {

 

​    /**

​     \* FTP

​     */

​    FTP {

​        /**

​         \* 获取枚举值

​         *

​         \* @return 枚举类型对应的数值

​         */

​        @Override

​        public int getValue() {

​            return 1;

​        }

 

​    },

 

​    /**

​     \* SFTP

​     */

​    SFTP {

​        /**

​         \* 获取枚举值

​         *

​         \* @return 枚举类型对应的数值

​         */

​        @Override

​        public int getValue() {

​            return 2;

​        }

 

​    },

 

​    /**

​     \* TFTP

​     */

​    TFTP {

​        /**

​         \* 获取枚举值

​         *

​         \* @return 枚举类型对应的数值

​         */

​        @Override

​        public int getValue() {

​            return 3;

​        }

 

​    },

 

​    /**

​     \* 其他类型

​     */

​    UNKNOWN {

​        /**

​         \* 获取枚举值

​         *

​         \* @return 枚举类型对应的数值

​         */

​        @Override

​        public int getValue() {

​            return 0;

​        }

 

​    };

 

​    /**

​     \* 获取枚举值

​     *

​     \* @return 枚举类型对应的数值

​     */

​    public abstract int getValue();

 

​    /**

​     \* 获取FTP类型

​     *

​     \* @param value

​     \*            1：FTP；2：SFTP；3TFTP

​     \* @return FTP类型

​     */

​    public static FTPType getType(final int value) {

​        switch (value) {

​        case 1:

​            return FTP;

 

​        case 2:

​            return SFTP;

 

​        case 3:

​            return TFTP;

 

​        default:

​            return UNKNOWN;

​        }

​    }

}

 

=====================================================================================================获取当前系统路径下具体文件的路径================================================================================================

public static String getDir(final String path, final String... fileNames)

​    {

​        if (null != path)

​        {

​            final StringBuffer buffer = new StringBuffer(path);

​            

​            if (null != fileNames)

​            {

​                for (final String fileName : fileNames)

​                {

​                    buffer.append(File.separator).append(fileName);

​                }

​            }

​            return buffer.toString();

​        }

​        return "";

​        

​    }

​    public static String getUserDir()

​    {

​        return System.getProperty("user.dir");

​    }

​    

​    /**

​     \* 获取当前系统路径下具体文件的路径

​     \* @param fileNames 文件名

​     \* @return 文件的路径

​     */

​    public static String getSystemUserDir(final String... fileNames)

​    {

​        return getDir(getUserDir(), fileNames);

​    }

=====================================================================================================观察者模式==============================================================================================

 

public final class ExceptionObservable extends Observable

{

​    

​    /**

​     \* 全局对象

​     */

​    private static volatile ExceptionObservable instance = null;

​    

​    private static volatile Object lock = new Object(); // must be declared volatile

​    

​    /**

​     \* 构造函数

​     */

​    private ExceptionObservable()

​    {

​        

​    }

​    

​    /**

​     \* 获取单体类对象

​     *

​     \* @return RunScriptConsole

​     */

​    public static ExceptionObservable getInstance()

​    {

​        synchronized (ExceptionObservable.lock)

​        {

​            if (instance == null)

​            {

​                instance = new ExceptionObservable();

​            }

​            return instance;

​        }

​        

​    }

​    

​    /**

​     \* <一句话功能简述>

​     \* <功能详细描述>

​     \* @param obj obj

​     \* @see [类、类#方法、类#成员]

​     */

​    public void notifyIt(Object obj)

​    {

​        setChanged();

​        notifyObservers(obj);

​    }

​    

}

 

 

 

 

ExceptionObservable.getInstance().addObserver(DownLoadSoftLogExtension.this);

 

public class DownLoadSoftLogExtension implements Observer

​    @Override

​    public void update(Observable o, Object arg)

​    {

​    }

​    

 

=====================================================================================================判断是否有同步操作在进行==============================================================================================

​    /**

​     \* 判断是否有同步操作在进行

​     \* @return boolean

​     */

​    public static boolean isSyncRunning()

​    {

​        boolean isRunning = !LOCK.tryLock();

​        try

​        {

​            return isRunning;

​        }

​        finally

​        {   

​            if (!isRunning)

​            {

​                LOCK.unlock();

​            }

​        }

​    }

 

=====================================================================================================行变列==============================================================================================

行变列

 

 

create table student(name varchar2(20),coursename varchar2(20),grade number(3));

 

insert into student values('rose','语文',86);

insert into student values('rose','数学',92);

insert into student values('rose','英语',75);

 

 

 

insert into student values('jack','语文',66);

insert into student values('jack','数学',82);

insert into student values('jack','英语',95);

 

现在要变成：

name    语文     数学    英语

rose    86       92      75

jack    66       82      95

 

 

 

 

select name,sum(decode(coursename,'语文',grade)) 语文,

sum(decode(coursename,'数学',grade)) 数学,

sum(decode(coursename,'英语',grade)) 英语 from  student

group by name

 

=====================================================================================================事务==============================================================================================

/**

​     \* 更新节点的额外信息，此处主要是记录使用的地图信息

​     \* @param id 节点唯一标识

​     \* @param userProps 额外信息

​     */

​    public void updateExtendAttr(String id, Map<String, Object> userProps)

​    {

​        final TransactionDefinition definition =

​            new DefaultTransactionDefinition(TransactionDefinition.PROPAGATION_REQUIRED);

​        final PlatformTransactionManager transActionManager = ServiceFactory.getInstance().getTransActionManager();

​        TransactionStatus transActionStatus = null;

​        

​        try

​        {

​            transActionStatus = transActionManager.getTransaction(definition);

​            

​            SiteDbUtil.deleteExtendAttr(id, userProps);

​            SiteDbUtil.insertExtendAttr(id, userProps);

​            

​            SiteTempCache.getInstance().updateExt(id, userProps);

​            

​            transActionManager.commit(transActionStatus);

​        }

​        catch (TransactionException e)

​        {

​            LOGGER.error("Failed to updateExtendAttr:", e);

​        }

​        catch (OMSException e)

​        {

​            LOGGER.error("Failed to updateExtendAttr:", e);

​        }

​        finally

​        {

​            if ((null != transActionStatus) && !transActionStatus.isCompleted())

​            {

​                try

​                {

​                    transActionManager.rollback(transActionStatus);

​                }

​                catch (final TransactionException e)

​                {

​                    LOGGER.error("updateExtendAttr,Roll back failed.e=", e);

​                }

​            }

​        }

​    }

​    

​    

我:

=====================================================================================================try==============================================================================================    

​    public class TestString

{

​    public static void main(String[] args)

​    {

​        System.out.println(test());

​    }

​    

​    public static int test()

​    {

​        int i = 9;

​        try

​        {

​            if (i > 6)

​            {

​                return i;

​            }

​        }

​        finally

​        {

​            System.out.println("cao ni ma ");

​        }

​        return 0;

​    }

}

 

结果：

cao ni ma

9

 

 

=====================================================================================================Properties==============================================================================================    

 

​        BufferedInputStream bufferedInputStream = null;

​        Properties properties = new Properties();

​        try

​        {

​            bufferedInputStream = new BufferedInputStream(new FileInputStream(OmuConstants.EIVS_OMU_INFO_FILE));

​            properties.load(bufferedInputStream);

​        }

​        catch (IOException e)

​        {

​            LOGGER.error("IOException");

​            throw new OMSException(ErrorCode.UCC_IVS_OMU_READ_PARAMS_ERROR, e);

​        }

​        finally

​        {

​            IOUtils.closeQuietly(bufferedInputStream);

​        }

​        

​        return properties.getProperty(param);

 

=====================================================================================================手动构造一段xml==============================================================================================    

<?xml version="1.0" encoding="utf-8"?>

<MESSAGE>

  <Content>

​    <NVRCode name="changzhichao">NVRCode</NVRCode>

​    <CameraCode id="37365">CameraCode</CameraCode>

​    <FromTime>FromTime</FromTime>

​    <ToTime>ToTime</ToTime>

  </Content>

</MESSAGE>

 

package org.jdom;

package org.jdom.output;

​        Element content = new Element("Content");

​        Element nVRCode = new Element("NVRCode").setText("NVRCode");

​        nVRCode.setAttribute("name", "changzhichao");

​        Element cameraCode = new Element("CameraCode").setText("CameraCode");

​        cameraCode.setAttribute("id", "37365");

​        Element fromTime = new Element("FromTime").setText("FromTime");

​        Element toTime = new Element("ToTime").setText("ToTime");

​        content.addContent(nVRCode);

​        content.addContent(cameraCode);

​        content.addContent(fromTime);

​        content.addContent(toTime);

​        

​        String xmlStr = null;

​        Element root = new Element("MESSAGE");

​        Document doc = new Document(root);

​        root.addContent(content);

​        

​        XMLOutputter outp = new XMLOutputter();

​        Format format = Format.getPrettyFormat();

​        format.setEncoding("utf-8");

​        outp.setFormat(format);

​        xmlStr = outp.outputString(doc);

​        System.out.println(xmlStr);

​        

​        

我:

=====================================================================================================HttpClient==============================================================================================            

 

HttpClient httpclient = new DefaultHttpClient();

 

HttpGet httpget = new HttpGet("[http://localhost/");](http://localhost/)

 

HttpResponse response = httpclient.execute(httpget);

 

HttpEntity entity = response.getEntity();

 

if (entity != null) {

 

InputStream instream = entity.getContent();

 

int l;

 

byte[] tmp = new byte[2048];

 

while ((l = instream.read(tmp)) != -1) {

 

}

 

}

 

HttpClient支持所有定义在HTTP/1.1版本中的HTTP方法：GET，HEAD，POST，PUT，DELETE，TRACE和OPTIONS。对于每个方法类型都有一个特殊的类：HttpGet，HttpHead，HttpPost，HttpPut，HttpDelete，HttpTrace和HttpOptions。

 

请求的URI是统一资源定位符，它标识了应用于哪个请求之上的资源。HTTP请求URI包含一个协议模式，主机名称，可选的端口，资源路径，可选的查询和可选的片段。

 

 

​        PostMethod post = new PostMethod(url);

​        httpClient.getParams().setParameter("https.socket.timeout", 15000);

​        httpClient.getParams().setParameter("https.connection.timeout", 15000);

​        httpClient.getParams().setParameter("https.connection-manager.timeout", CONN_MANAGER_TIMEOUT);

​        repCode = httpClient.executeMethod(post);

​        if (repCode == 200)

​        {

​            resultData = httpClientManager.getResponseMsg(post);

​        }

​        

​        public String getResponseMsg(PostMethod postMethod)

​        {

​        LOGGER.debug("getResponseMsg: {}", postMethod);

​        String res = null;

​        try

​        {

​            byte[] body = postMethod.getResponseBody();

​            res = new String(body, "utf-8");

​            LOGGER.debug("resultData = {}", res);

​        }

​        catch (UnsupportedEncodingException e)

​        {

​            LOGGER.error("UnsupportedEncodingException,E=", e);

​        }

​        catch (IOException e)

​        {

​            LOGGER.error("IOException,E=", e);

​        }

​        finally

​        {

​            postMethod.releaseConnection();

​        }

​        

​        return res;

​        }

=====================================================================================================Https============================================================================================

 

2：url：地址  sendData：发送的XML

public static String doPostSync(String url, String sendData)

​    {

​        String resultData = null;

​        int repCode = 0;

​        HttpClient httpClient = null;

​        try

​        {

​            httpClient = httpClientManager.getDefaultHttpClient();

​        }

​        catch (OMSException e1)

​        {

​            LOGGER.error("getDefaultHttpClient failed.e1=", e1);

​            return resultData;

​        }

​        PostMethod post = httpClientManager.getHttpPost(url, sendData);

​        httpClient.getHttpConnectionManager().getParams().setConnectionTimeout(15000);

​        httpClient.getHttpConnectionManager().getParams().setSoTimeout(300000);

​        try

​        {

​            repCode = httpClient.executeMethod(post);

​        }

​        catch (HttpException e)

​        {

​            LOGGER.error("executeMethod HttpException,e=", e);

​            return resultData;

​        }

​        catch (IOException e)

​        {

​            LOGGER.error("executeMethod IOException,e=", e);

​            return resultData;

​        }

​        

​        if (repCode == 200)

​        {

​            resultData = httpClientManager.getResponseMsg(post);

​        }

​        else

​        {

​            LOGGER.error("omu response error");

​        }

​        

​        return resultData;

​    }

​    

​    package com.huawei.oms.esight.ucc.ivs.omu.channel.http;

 

import java.io.IOException;

import java.io.UnsupportedEncodingException;

 

import org.apache.commons.httpclient.HttpClient;

import org.apache.commons.httpclient.methods.PostMethod;

import org.apache.commons.httpclient.protocol.Protocol;

 

import com.huawei.oms.esight.ucc.ivs.omu.channel.utils.PropertiesMgr;

import com.huawei.oms.exception.OMSException;

import com.huawei.oms.log.Logger;

import com.huawei.oms.ucc.common.util.anonymize.OMSLogFactory;

 

/**

*

\* HttpClient单例管理器 描述：

\* <p>

\* 实例化<br>

\* 全局有且仅有一个<br>

\* 作者： s00209686 创建时间： 2013-1-31-下午6:42:55

*

\* @see 相关类或方法

\* @since eSightUCC V100R001C01 修订说明：

\*        <p>

\*        修订说明第一行<br>

\*        修订说明第二行<br>

*/

public class HttpClientManager

{

​    /**

​     \* HTTPS

​     */

​    public static final String HTTPS = "https";

​    

​    /**

​     \* 日志对象

​     */

​    private static final Logger LOGGER = OMSLogFactory.getLog(HttpClientManager.class);

​    

​    /**

​     \* HttpClient管理器单例

​     */

​    private static HttpClientManager instance = null;

​    

​    /**

​     *

​     \* 构造方法说明

​     *

​     \* @see 相关类或方法

​     */

​    public HttpClientManager()

​    {

​        LOGGER.info("HttpClientManager Constructors");

​    }

​    

​    /**

​     \* 获取单例。

​     *

​     \* @return HttpClientManager 单例

​     \* @see [类、类#方法、类#成员]

​     */

​    public static synchronized HttpClientManager getInstance()

​    {

​        if (null == instance)

​        {

​            instance = new HttpClientManager();

​        }

​        

​        return instance;

​    }

​    

​    /**

​     \* 实例化一个HttpClient

​     \* @return HttpClient

​     \* @throws OMSException OMSException

​     */

​    @SuppressWarnings("deprecation")

​    public HttpClient getDefaultHttpClient()

​        throws OMSException

​    {

​        LOGGER.info("initializing https client...");

​        //        //模拟桩测试联通，真实数据联通，MainOmuInfo.java中的 EamManager.getNodeService()出错

​        //        int httpsPort = 8448;

​        int httpsPort = Integer.parseInt(PropertiesMgr.getInstance().getPort());

​        

​        Protocol httpsProtocol = new Protocol("https", new IVSSecureProtocolSocketFactory(), httpsPort);

​        Protocol.registerProtocol(HTTPS, httpsProtocol);

​        HttpClient httpsClient = new HttpClient();

​        LOGGER.debug("init https client : {}", httpsClient);

​        return httpsClient;

​    }

​    

​    /**

​     \* 封装post请求

​     *

​     \* @param url

​     \*            连接地址

​     \* @param sendData

​     \*            发送数据

​     \* @return PostMethod

​     \* @author y00208965

​     \* @since eSightUCC V100R001C01

​     */

​    @SuppressWarnings("deprecation")

​    public PostMethod getHttpPost(String url, String sendData)

​    {

​        PostMethod post = new PostMethod(url);

​        // 设置数据格式和编码

​        post.addRequestHeader("Content-Type", "text/xml;Charset=UTF-8");

​        post.setRequestBody(sendData);

​        return post;

​    }

​    

​    /**

​     \* 获取响应

​     *

​     \* @param postMethod

​     \*            PostMethod

​     \* @return String

​     \* @author y00208965

​     \* @since eSightUCC V100R001C01

​     */

​    public String getResponseMsg(PostMethod postMethod)

​    {

​        LOGGER.debug("getResponseMsg: {}", postMethod);

​        String res = null;

​        try

​        {

​            byte[] body = postMethod.getResponseBody();

​            res = new String(body, "utf-8");

​            LOGGER.debug("resultData = {}", res);

​        }

​        catch (UnsupportedEncodingException e)

​        {

​            LOGGER.error("UnsupportedEncodingException,E=", e);

​        }

​        catch (IOException e)

​        {

​            LOGGER.error("IOException,E=", e);

​        }

​        finally

​        {

​            postMethod.releaseConnection();

​        }

​        

​        return res;

​    }

​    

}

我:

=====================================================================================================Properties==============================================================================================    

采用Thread.currentThread().getContextClassLoader().getResourceAsStream(file)的方式读取

 

​        String file = "test.properties";

 

​        Properties localProperties1 = new Properties();

 

​        InputStream localInputStream = Thread.currentThread().getContextClassLoader().getResourceAsStream(file);

 

​        System.out.println("hhh");

 

​         try {

 

​            localProperties1.load(localInputStream);

 

​        } catch (IOException e) {

 

​            // TODO Auto-generated catch block

 

​            e.printStackTrace();

 

​        }

​        

​        

​        InputStream in = null;

​        File file = new File(FILE_PATH);

​        if (!file.exists())

​        {

​            try

​            {

​                FileUtils.touch(file);

​            }

​            catch (IOException e)

​            {

​                LOGGER.error("IOException happened when read ivs topo dao file.");

​            }

​            LOGGER.debug("create NewFile for locations end.");

​            return;

​        }

​        

​        try

​        {

​            in = new BufferedInputStream(new FileInputStream(FILE_PATH));

​            PROPERTIES.load(in);   // 将属性文件流装载到Properties对象中

​        }

​        catch (IOException e)

​        {

​            LOGGER.error("IOException happened when read ivs topo dao file.");

​        }

​        finally

​        {

​            IOUtils.closeQuietly(in);

​        }

​        LOGGER.debug("Load locations end, size: {}", PROPERTIES.size());

 

 

=====================================================================================================观察者模式==============================================================================================    

public class ViewTest extends Observable

{

​    private String name;

​    

​    public ViewTest(String name)

​    {

​        this.name = name;

​    }

​    

​    public void start()

​    {

​        int rand = new Random().nextInt() % 5 + 5;

​        boolean result = rand % 3 > 0;

​        while (rand-- > 0)

​        {

​            System.out.println("PipeServise(" + this.name + ")正在执行");

​            try

​            {

​                Thread.sleep(1000);

​            }

​            catch (InterruptedException e)

​            {

​                // TODO Auto-generated catch block

​                e.printStackTrace();

​            }

​        }

​        this.runFinisg(result);

​    }

 

​    private void runFinisg(boolean result)

​    {

​        this.setChanged();

​        this.notifyObservers("PipeServise(" + this.name + ")正在执行 " + String.valueOf(result));

​        

​    }

}

 

public class ViewChang implements Observer

{

​    private String name;

​    

​    public ViewChang(String name)

​    {

​        super();

​        this.name = name;

​    }

​    

​    @Override

​    public void update(Observable o, Object arg)

​    {

​        // TODO Auto-generated method stub

​        

​        System.out.println("观察者" + name + "收到通知:" + String.valueOf(arg));

​        

​    }

}

 

public class Test

{

​    public static void main(String[] args)

​    {

​        ViewTest t1 = new ViewTest("project1");

​        t1.addObserver(new ViewChang("chang"));

​        t1.addObserver(new ViewChang("zhi"));

​        t1.addObserver(new ViewChang("chao"));

​        

​        ViewTest t2 = new ViewTest("project2");

​        t2.addObserver(new ViewChang("chang"));

​        t2.addObserver(new ViewChang("zhi"));

​        t2.addObserver(new ViewChang("chao"));

​        

​        t1.start();

​        t2.start();

​    }

}

 

 

=====================================================================================================PriorityQueue========================================================================================

public class BookComparator implements Comparator<Book>

{

​    @Override

​    public int compare(Book o1, Book o2)

​    {

​        return o1.getId() - o2.getId();

​    }

}

 

​    public static void main(String[] args)

​    {

​        Queue<Integer> priorityQueue = new PriorityQueue<Integer>();

​        

​        priorityQueue.offer(1);

​        priorityQueue.offer(3);

​        priorityQueue.offer(2);

​        priorityQueue.offer(4);

​        

​        System.out.println(priorityQueue.poll());

​        System.out.println(priorityQueue.poll());

​        System.out.println(priorityQueue.poll());

​        System.out.println(priorityQueue.poll());

​        

​        System.out.println("------------------->");

​        

​        Queue<Book> priorityQueue2 = new PriorityQueue<Book>(4, new BookComparator());

​        Book bk1 = new Book(1, "1", 1L);

​        Book bk2 = new Book(2, "2", 2L);

​        Book bk3 = new Book(3, "3", 3L);

​        Book bk4 = new Book(4, "4", 4L);

​        priorityQueue2.offer(bk1);

​        priorityQueue2.offer(bk4);

​        priorityQueue2.offer(bk2);

​        priorityQueue2.offer(bk3);

​        

​        System.out.println(priorityQueue2.poll());

​        System.out.println(priorityQueue2.poll());

​        System.out.println(priorityQueue2.poll());

​        System.out.println(priorityQueue2.poll());

​    }

​    结果：

1

2

3

4

------------------->

Book [id=1, name=1, price=1]

Book [id=2, name=2, price=2]

Book [id=3, name=3, price=3]

Book [id=4, name=4, price=4]

 

 

 

 

 

Pair<String,Integer> a0 = new MutablePair <String,Integer>("当日达",0);

​        Pair<String,Integer> a1 = new MutablePair <String,Integer>("次日达",0);

​        Pair<String,Integer> a2 = new MutablePair <String,Integer>("隔日达",0);

​        Pair<String,Integer> a3 = new MutablePair <String,Integer>("三日达",0);

​        Pair<String,Integer> a4 = new MutablePair <String,Integer>("四日达",0);

​        Pair<String,Integer> a5 = new MutablePair <String,Integer>("五日达",0);

​        Pair<String,Integer> a6 = new MutablePair <String,Integer>("六日达",0);

​        Pair<String,Integer> a7 = new MutablePair <String,Integer>("七日达",7);

​        Queue<Pair> priorityQueue = new PriorityQueue<Pair>(8, new PairComparator());

​        

​        priorityQueue.offer(a0);

​        priorityQueue.offer(a1);

​        priorityQueue.offer(a2);

​        priorityQueue.offer(a3);

​        priorityQueue.offer(a4);

​        priorityQueue.offer(a5);

​        priorityQueue.offer(a6);

​        priorityQueue.offer(a7);

class PairComparator implements Comparator<Pair>{

​    @Override

​    public int compare(Pair o1, Pair o2) {

​        return Integer.parseInt(o2.getValue().toString()) - Integer.parseInt(o1.getValue().toString());

​    }

}

 

补充：

Pair o1, Pair o2

o2.compareTo(o1)   Compares the pair based on the left element followed by the right element.

结果：  [(七日达,7), (当日达,0), (隔日达,0), (次日达,0), (四日达,0), (五日达,0), (六日达,0), (三日达,0)]     //对于都是0的情况没有按照原来默认的顺序排序。当日达 没有在 次日达 前面。

 

 

如果要按照默认的顺序升序：冒泡排序

​        Pair<String, Integer> a0 = new MutablePair<String, Integer>("当日达", 0);

​        Pair<String, Integer> a1 = new MutablePair<String, Integer>("次日达", 0);

​        Pair<String, Integer> a2 = new MutablePair<String, Integer>("隔日达", 0);

​        Pair<String, Integer> a3 = new MutablePair<String, Integer>("三日达", 0);

​        Pair<String, Integer> a4 = new MutablePair<String, Integer>("四日达", 0);

​        Pair<String, Integer> a5 = new MutablePair<String, Integer>("五日达", 0);

​        Pair<String, Integer> a6 = new MutablePair<String, Integer>("六日达", 0);

​        Pair<String, Integer> a7 = new MutablePair<String, Integer>("七日达", 7);

​        List<Pair<String, Integer>> pairList = new ArrayList<Pair<String, Integer>>(8);

​        pairList.add(a0);

​        pairList.add(a1);

​        pairList.add(a2);

​        pairList.add(a3);

​        pairList.add(a4);

​        pairList.add(a5);

​        pairList.add(a6);

​        pairList.add(a7);

​        bubbleSort(pairList);

​        System.out.println(pairList);

 

​    public static void bubbleSort(List<Pair<String, Integer>> pairList) {

​        Pair<String, Integer> temp = new MutablePair<String, Integer>();

​        int size = pairList.size();

​        for (int i = 0; i < size - 1; i++) {

​            for (int j = size - 1 - i; j > 0; j--) {

​                if (Integer.parseInt(pairList.get(j).getValue().toString()) > Integer

​                        .parseInt(pairList.get(j - 1).getValue().toString())) // 交换两数位置

​                {

​                    temp = pairList.get(j);

​                    pairList.set(j, pairList.get(j - 1));

​                    pairList.set(j - 1, temp);

​                }

​            }

​        }

​    }

=====================================================================================================相对路径========================================================================================

​        tableView.getStylesheets().add("file:" + System.getProperty("user.dir").replace("\\", "/")

​            \+ "/src/main/resources/config/tableView.css");

​            

System.getProperty("user.dir")：

如果事web项目，这个System.getProperty("user.dir")的结果，就是tomcat的bin目录，这是在项目启动的时候，我是tomcat容器，所以，这个就是的结果就是tomcat的bin目录，

要是简单的main方法的测试，那就是你这个项目的工作目录。就是项目的绝对路径。还有就是jar包的工程，也是项目的绝对地址。

String uploadPath = getContext().getServletContext().getRealPath("/") 用这个来代替 System.getProperty("user.dir")：

 

System.getProperty("user.dir");

右击此程序选择run as application ：

D:\JAVA\Hellios\IDENewWorkSpace\KmProject\WebContent\upload\

放到后台的类里面后结果竟然变成了：

D:\JAVA\Hellios\eclipse-jee-helios-win32\eclipse\WebContent\upload\

也就是说我在run as application 的时候得到的是项目所在的路径，也是我要的。但是在run as server 的时候的变成了eclipse的安装路径了。

 

=====================================================================================================内部类========================================================================================

 

public class BiikTest

{

​    public BiikTest()

​    {

​        

​    }

​    

​    class A

​    {

​        public A()

​        {

​            

​        }

​        

​        public boolean equals(Object obj)

​        {

​            return true;

​        }

​    }

​    

​    //类B的hashCode()方法总是返回1,但没有重写其equals()方法。不能保证当前对象是HashSet中的唯一对象

​    class B

​    {

​        public int hashCode()

​        {

​            return 1;

​        }

​    }

​    

​    //类C的hashCode()方法总是返回2,且有重写其equals()方法

​    class C

​    {

​        public int hashCode()

​        {

​            return 2;

​        }

​        

​        public boolean equals(Object obj)

​        {

​            return true;

​        }

​    }

​    

​    @SuppressWarnings("unchecked")

​    public static void main(String[] args)

​    {

​        HashSet books = new HashSet();

​        BiikTest te = new BiikTest();

​        //分别向books集合中添加两个A对象，两个B对象，两个C对象

​        books.add(te.new A());

​        books.add(te.new A());

​        

​        books.add(te.new B());

​        books.add(te.new B());

​        

​        books.add(te.new C());

​        books.add(te.new C());

​        System.out.println(books);

​    }

}

 

 

[com.huawei.oms.esight.ucc.ivs.offline.BiikTest$B@1, com.huawei.oms.esight.ucc.ivs.offline.BiikTest$B@1, com.huawei.oms.esight.ucc.ivs.offline.BiikTest$C@2, com.huawei.oms.esight.ucc.ivs.offline.BiikTest$A@121f956, com.huawei.oms.esight.ucc.ivs.offline.BiikTest$A@17b5179]

我:

=====================================================================================================TreeSet========================================================================================

public static void main(String[] args)

​    {

​        TreeSet nums = new TreeSet();

​        //向TreeSet中添加四个Integer对象

​        nums.add(5);

​        nums.add(2);

​        nums.add(10);

​        nums.add(-9);

​        

​        //输出集合元素，看到集合元素已经处于排序状态

​        System.out.println(nums);

​        

​        //输出集合里的第一个元素

​        System.out.println(nums.first());

​        

​        //输出集合里的最后一个元素

​        System.out.println(nums.last());

​        

​        //返回小于4的子集，不包含4

​        System.out.println(nums.headSet(4));

​        

​        //返回大于5的子集，如果Set中包含5，子集中还包含5

​        System.out.println(nums.tailSet(5));

​        

​        //返回大于等于-3，小于4的子集。

​        System.out.println(nums.subSet(-3, 4));

​    }

​    

结果：

[-9, 2, 5, 10]

-9

10

[-9, 2]

[5, 10]

[2]

 

TreeSet用来排序，截取其中特定一段

 

public class Book implements Comparable

{

​    private int id;

​    

​    private String name;

​    

​    private Long price;

​    

​    @Override

​    public int compareTo(Object o)

​    {

​        final Book othSiteModel = (Book)o;

​        return this.id - othSiteModel.getId();

​    }

}

 

​        TreeSet<Book> nk = new TreeSet<Book>();

​        Book bk1 = new Book(1, "1", 1l);

​        Book bk3 = new Book(3, "3", 3l);

​        Book bk2 = new Book(2, "2", 2l);

​        Book bk4 = new Book(4, "4", 4l);

​        nk.add(bk1);

​        nk.add(bk3);

​        nk.add(bk2);

​        nk.add(bk4);

​        System.out.println(nk);

​        

​        //输出集合里的第一个元素

​        System.out.println(nk.first());

​        

​        //输出集合里的最后一个元素

​        System.out.println(nk.last());

​        

​        System.out.println(nk.headSet(bk2));

​        

​        //返回大于5的子集，如果Set中包含5，子集中还包含5

​        System.out.println(nk.tailSet(bk2));

​        

​        //返回大于等于-3，小于4的子集。

​        System.out.println(nk.subSet(bk1, bk3));

​        

结果：

[Book [id=1, name=1, price=1], Book [id=2, name=2, price=2], Book [id=3, name=3, price=3], Book [id=4, name=4, price=4]]

Book [id=1, name=1, price=1]

Book [id=4, name=4, price=4]

[Book [id=1, name=1, price=1]]

[Book [id=2, name=2, price=2], Book [id=3, name=3, price=3], Book [id=4, name=4, price=4]]

[Book [id=1, name=1, price=1], Book [id=2, name=2, price=2]]

 

定制排序：

TreeSet ts = new TreeSet(new Comparator()

​        {

​            //根据M对象的age属性来决定大小

​            public int compare(Object o1, Object o2)

​            {

​                M m1 = (M)o1;

​                M m2 = (M)o2;

​                return m1.age > m2.age ? -1

​                    : m1.age < m2.age ? 1 : 0;

​            }

​        });

​        

​        SortedSet s = Collections.synchronizedSortedSet(new TreeSet(...));

=====================================================================================================String的equals========================================================================================

​    public static void main(String[] args)

​    {

​        String a = "a";

​        String b = "a";

 

​        String c = new String("a");

​        String d = new String("a");

​        System.out.println(a.equals(b));

​        System.out.println(c.equals(d));

​        System.out.println(c.equals(a));

​        System.out.println(c.equals(d));

​    }

​    结果：

​    全部true

 

String既可以作为一个对象来使用，又可以作为一个基本类型来使用。

基本类型来使用只是指使用方法上的，比如String s = "Hello"

而作为一个对象来使用，则是指通过new关键字来创建一个新对象，比如String s = new String("Hello")

一种是用"=="来比较，这种比较是针对两个String类型的变量的引用，也就是说如果两个String类型的变量，

它们所引用同一个String对象(即指向同一块内存堆)，则"=="比较的结果是true。

 

另一种是用Object对象的equals()方法来比较，String对象继承自Object，

并且对equals()方法进行了重写。两个String对象通过equals()方法来进行比较时，

其实就是对String对象所封装的字符串内容进行比较，也就是说如果两个String对象所封装的字符串内容相同(包括大小写相同)，

则equals()方法将返回true。

---------------------------------------------------------》

String s1 = new String("Hello");

String s2 = s1;

System.out.println(s1 == s2);

System.out.println(s1.equals(s2));

以上代码段的打印结果是：

true

true

---------------------------------------------------------》

String s1 = "Hello";

String s2 = "Hello";

System.out.println(s1 == s2);

System.out.println(s1.equals(s2));

以上代码段的打印结果是：

true

true

首先这两个String对象都是作为一个基本类型来使用的，

而不是通过new关键字来创建的，因此虚拟机不会为这两个String对象分配新的内存堆，而是到String缓冲池中来寻找。

首先为s1寻找String缓冲池内是否有与"Hello"相同值的String对象存在，此时String缓冲池内是空的，没有相同值的String对象存在，所以虚拟机会在String缓冲池内创建此String对象，其动作就是new String("Hello");。然后把此String对象的引用赋值给s1

接着为s2寻找String缓冲池内是否有与"Hello"相同值的String对象存在，此时虚拟机找到了一个与其相同值的String对象，这个String对象其实就是为s1所创建的String对象。既然找到了一个相同值的对象，那么虚拟机就不在为此创建一个新的String对象，而是直接把存在的String对象的引用赋值给s2。

 

如果：

String s1 = new String("Hello");

String s2 = new String("Hello");

两个String类型的变量s1和s2都通过new关键字分别创建了一个新的String对象，这个new关键字为创建的每个对象分配一块新的、独立的内存堆。因此当通过"=="来比较它们所引用的是否是同一个对象时，将返回false。

 

只要一个对象是new的，那么就会在堆空间为其开辟空间

 

=====================================================================================================JSON字符串转对象======================================================================================

​    public static <T> T strToObj(String string, final Class<T> class1)

​        throws OMSException

​    {

​        ObjectMapper mapper = new ObjectMapper();

​        T result = null;

​        try

​        {

​            result = mapper.readValue(string, class1);

​        }

​        catch (JsonParseException e)

​        {

​            LOGGER.error("JsonGenerationException occur");

​            throw new OMSException("exception is:", e);

​        }

​        catch (JsonMappingException e)

​        {

​            LOGGER.error("JsonMappingException occur");

​            throw new OMSException("exception is:", e);

​        }

​        catch (IOException e)

​        {

​            LOGGER.error("IOException occur");

​            throw new OMSException("IOException", e);

​        }

​        return result;

​    }

我:

===================================================================================================interrupt唤醒sleep线程==================================================================================

public class ThreadTest extends Thread

{

​    private volatile boolean finished = false;

​    

​    public void stopMe()

​    {

​        finished = true;

​        System.out.println("now finished:" + finished);

​        this.interrupt(); //① 产生一个中断

​    }

​    

​    @Override

​    public void run()

​    {

​        while (!finished)

​        {

​            System.out.println("finished:" + finished);

​            long b = System.currentTimeMillis();

​            try

​            {

​                Thread.currentThread().sleep(6000);

​            }

​            catch (InterruptedException e)

​            {

​                System.out.println("InterruptedException happens one");

​            }

​            

​            long a = System.currentTimeMillis();

​            System.out.println("当前线程执行完成一次:" + (a - b));

​            try

​            {

​                Thread.currentThread().sleep(6000);

​            }

​            catch (InterruptedException e)

​            {

​                System.out.println("InterruptedException happens two");

​            }

​            System.out.println("当前线程执行完成2次 : " + (System.currentTimeMillis() - a));

​        }

​    }

}

 

public static void main(String[] args)

{

​        ThreadTest threadTest = new ThreadTest();

​        threadTest.start();

​        try

​        {

​            Thread.sleep(1000 * 1); //主线程睡1秒

​        }

​        catch (InterruptedException e)

​        {

​        }

​        threadTest.stopMe();

}

 

结果：

finished:false

now finished:true

InterruptedException happens one

当前线程执行完成一次:1002

当前线程执行完成2次 : 6008

===============================================================================线程保护===================================================================================

必须对线程保护，防止线程崩溃。建议使用try-catch 或 Thread.setDefaultUncaughtExceptionHandle 方法来做

多线程并发时应避免被频繁的锁在同一处，导致同步等待，使用减少临界区、分拆临界资源、缓存避免被锁定 等来提升并发效率

不要把资源消耗或耗时（计算、IO）相差很大的逻辑放到一个线程中处理，可以使用流水线（生产者消费者）方式多线程并发处理

不要使用Thread.stop方法退出线程

不要依赖线程调度器、线程优先级和yield() 方法来决定程序的逻辑，应为java中线程调度依赖操作系统以及JVM的实现，会导致不可移植

 

===============================================================================构造XML===================================================================================

StringBuffer sb = new StringBuffer("<?xml version=\"1.0\" encoding =\"utf-8\"?>" + "\n");

sb.append("<MESSAGE>" + "\n");

 

===============================================================================自己的日志===================================================================================

import java.text.SimpleDateFormate;

import java.util.Date;

import java.util.logging.FileHandler;

import java.util.logging.Level;

import java.util.logging.Logger;

import java.util.logging.SimpleFormatter;

public class LoggerUtil{

  private static String getLogName(){

​     StringBuffer logPath = new StringBuffer();

​     logPath.append(System.getProperty("user.home"));

​     logPath.append("\\" + "My");

​     File file = new File(logPath.toString()); //file是个文件夹路径

​     if(!file.exists()){

​         file.mkdir();

​     }

​     SimpleDateFormate sdf = new SimpleDateFormate("yyyy-MM-dd");

​     logPath.append("\\" + sdf.format(new Date()) + ".log");

​     return logPath.toString();

  }

  public static void setLogingProperties(Logger lgger){

​     setLogingProperties(lgger,Level.ALL);

  }

  public static void setLogingProperties(Logger lgger , Level level){

​     FileHandler fh = new FileHandler(getLogName(),true);

​     lgger.addHandler(fh);

​     fh.setFormatter(new SimpleFormatter());

​     //lgger.setLevel(level);

  }

  public LogLevel getLogLevel(){

​     Level level = logger.getEffectiveLevel();

​     if(Level.DEBUG.equals(level)){

​         return LogLevel.DEBUG;

​     }

​     ......

  }

  main(){

​     Logger logger = Logger.getLogger(LoggerUtil.class.getName());

​     LoggerUtil.setLogingProperties(logger);

​     logger.log(Level.INFO,"AAA");

​     logger.log(Level.INFO,"BBB");

  }

}

===================================================================================================获取本地IP===================================================================================

String localIP = InetAddress.getLocalHost().getHostAddress();

 

===================================================================================================java反射===================================================================================

@Path("dbsource")

public class DBSourceRest{}

 

Object obj = Class.forName("com.huawei.DBSourceRest").newInstance();

Path clsPath = obj.getClass().getAnnotation(Path.class);

String clsPathValue = clsPath.value(); //dbsource

 

Method[] methods = obj.getClass().getDeclaredMethods();

for(Method m : methods){

​    if(m.getAnnotation(Get.class) != null){

​     ....

​    }

}

 

===================================================================================================String的三位小数截取===================================================================================

float money = 12.1239f;

 

NumberFormat form = new DecimalFormat(".000");

String m = form.format(money);

 

法2：

final String p = "%.3f"；

String.format(p,money);

===================================================================================================MessageFormat===================================================================================

public String getInfo(){

   return MessageFormat.format("A={0},B={1},C={2}",this.getA(),this.getB(),this.getC());

}

===================================================================================================静态的思想===================================================================================

private static String localAddr = null;

public static String getLocalAdde(){

​    if(null == localAddr){

​        localAddr = ..;

​    }

​    return localAddr;

}

===================================================================================================String.valueOf===================================================================================

char[] b = new char[]{'1','2','3','4'};

String.valueOf(b)    //1234

String.valueOf(b,1,2)  //23

===================================================================================================动态加载内容===================================================================================

如果我想在运行中改变参数且能够生效：

PropertiesConfiguration cog = new PropertiesConfiguration(A.class.getResource("/a.properties"));

cog.setReloadingStrategy(new FileChangeReloadingStrategy());

===================================================================================================判断系统是windows还是linux===================================================================================

String os = System.getProperty("os.name").toLowCase();  //windows7

例子：

Process p = null;

if(os.indexOf("windows") > -1){

   p = Runtime.getRuntime().exec("cmd /c set");

}else{

   p = Runtime.getRuntime().exec("/bin/sh -c set");

}

 

 

===================================================================================================interrupt唤醒wait线程===================================================================================

public class ThreadTest extends Thread

{

​    private volatile boolean finished = false;

​    

​    private Object obj = new Object();

​    

​    public void stopMe()

​    {

​        finished = true;

​        System.out.println("now finished:" + finished);

​        this.interrupt(); //① 产生一个中断

​    }

​    

​    @Override

​    public void run()

​    {

​        while (!finished)

​        {

​            System.out.println("finished:" + finished);

​            long b = System.currentTimeMillis();

​            synchronized (obj)

​            {

​                try

​                {

​                    obj.wait();

​                }

​                catch (InterruptedException e)

​                {

​                    // TODO Auto-generated catch block

​                    e.printStackTrace();

​                }

​            }

​            long a = System.currentTimeMillis();

​            System.out.println("当前线程执行完成一次:" + (a - b));

​            try

​            {

​                Thread.currentThread().sleep(6000);

​            }

​            catch (InterruptedException e)

​            {

​                

​            }

​            System.out.println("当前线程执行完成2次 : " + (System.currentTimeMillis() - a));

​        }

​    }

}

public static void main(String[] args)

{

​        ThreadTest threadTest = new ThreadTest();

​        threadTest.start();

​        try

​        {

​            Thread.sleep(1000 * 1); //主线程睡1秒

​        }

​        catch (InterruptedException e)

​        {

​        }

​        threadTest.stopMe();

}

 

结果：

finished:false

now finished:true

java.lang.InterruptedException

当前线程执行完成一次:1002

​    at java.lang.Object.wait(Native Method)

​    at java.lang.Object.wait(Object.java:503)

​    at com.huawei.oms.esight.ucc.ivs.topo.ds.service.impl.ThreadTest.run(ThreadTest.java:28)

当前线程执行完成2次 : 6013

 

错误场景： IllegalMonitorStateException，wait的调用者必须是锁对象

public class ThreadTest extends Thread

{

​    private volatile boolean finished = false;

​    

​    private Object obj = new Object();

​    

​    public void stopMe()

​    {

​        finished = true;

​        System.out.println("now finished:" + finished);

​        this.interrupt(); //① 产生一个中断

​    }

​    

​    @Override

​    public void run()

​    {

​        while (!finished)

​        {

​            System.out.println("finished:" + finished);

​            long b = System.currentTimeMillis();

​            synchronized (obj)

​            {

​                try

​                {

​                    //Thread.currentThread().wait();

​                    //wait();

​                    //this.wait();

​                    obj.wait();

​                }

​                catch (InterruptedException e)

​                {

​                    // TODO Auto-generated catch block

​                    e.printStackTrace();

​                }

​            }

​            long a = System.currentTimeMillis();

​            System.out.println("当前线程执行完成一次:" + (a - b));

​            try

​            {

​                Thread.currentThread().sleep(6000);

​            }

​            catch (InterruptedException e)

​            {

​                

​            }

​            System.out.println("当前线程执行完成2次 : " + (System.currentTimeMillis() - a));

​        }

​    }

}

public static void main(String[] args)

{

​        ThreadTest threadTest = new ThreadTest();

​        threadTest.start();

​        try

​        {

​            Thread.sleep(1000 * 1); //主线程睡1秒

​        }

​        catch (InterruptedException e)

​        {

​        }

​        threadTest.stopMe();

}

 

结果：

finished:false

Exception in thread "Thread-0" java.lang.IllegalMonitorStateException

​    at java.lang.Object.wait(Native Method)

​    at java.lang.Object.wait(Object.java:503)

​    at com.huawei.oms.esight.ucc.ivs.topo.ds.service.impl.ThreadTest.run(ThreadTest.java:30)

now finished:true

 

===================================================================================================泛型的思想===================================================================================

public class Pair<T1,T2> implements Serializable{

​     private static final long serialVersionUID = xxxL;

​     private T1 fir;

​     private T2 sec;

}

用法：

List<Pair<C1,C2>> xx = null;

 

泛型类：

public class Pair<T, U> {

​    private T first;

​    private U second;

​    public Pair(T first, U second) {

​        this.first = first;

​        this.second = second;

​    }

​    public T getFirst() {

​        return first;

​    }

​    public U getSecond() {

​        return second;

​    }

​    public void setFirst(T newValue) {

​        first = newValue;

​    }

​    public void setSecond(U newValue) {

​        second = newValue;

​    }

}

 

泛型方法：

​    public static <T> T getMiddle(T[] a) {

​        return a[a.length / 2];

​    }

​    

===================================================================================================Pair与Map===================================================================================

Map是一个容器，Pair是一个对象

 

Pair类在javafx.util 包中，类构造函数有两个参数，键及对应值：

​    Pair<Integer, String> pair = new Pair<>(1, "One");

​    Integer key = pair.getKey();

​    String value = pair.getValue();

 

 

===================================================================================================组合索引===================================================================================

1.如果多个字段经常一起出现在where条件中，那么建议将它们创建为组合索引

2.如果组合索引中某个字段也会单独出现在where条件中，那么建议将该字段放在索引定义的第一位；尽量把最常用的字段放前面，离散值高的字段往前面放

查询时，有的列是非等值条件，有的列是等值条件，等值条件字段放前面

 

===================================================================================================汪天佑===================================================================================

form：前台通过servlet向后台请求，后台再怎么向前台交互呢？

后台拼接一个js给前台执行：这个JS要包在<head>里

  

   <head>

​       <metahttp-equiv = "Content-Type" content = "text/html;charset = utf-8"/>

       <script type
= "text/javascript">

​           window.location  = xxxx;

​       </script>    

   </head>

 

思想：返回一个js给前台执行，让他刷新页面，再在刷新页面的代码里实现逻辑

 

servlet的逻辑里：

public void doGet(HttpServletRequest request,HttpServletResponse response){

​    request.setCharacterEncoding("utf-8");

​    response.setContentType("text/html;charset = utf-8");

​    String str = "<head><metahttp-equiv = \"Content-Type\" content = \"text/html;charset = utf-8\"/>" + .....

​    

​    PrintWriter pw = response.getWriter();

​    pw.append(str);

​    pw.flush();

​    pw.close();

}   

 

===============================================================================JSON===================================================================================

1.JSONArray

JSONArray jsonArr = JSONArray.formObject(str);

int size = jsonArr.size();

for(int i=0;i<size ; i++){

   JSONObject o = jsonArr.getJSONObject(i);

}

 

JSONObject jsonObj = JSONObject.formObject(str2);

StressTaskClass cc = (StressTaskClass)JSONObject.toBean(jsonObj,StressTaskClass.class);

 

2.前台往后台传参数，json要Stringfy

var obj = {

   typeList : typeList

};

var str = JSON.stringfy(obj);

 

data:{

   items : str

}

JSON参数Key对应的value一定是字符串：

items : '{"typeList":["a","b"],"percent":40,"uoaList":"cc"}'

 

public String getAttribute(HttpServletRequest request,String key){

​    Object val = request.getAttribute(key);

​    if(null != val){

​        return String.valueOf(val).trim();

​    }else{

​        String val2 = request.getParameter(key);

​        if(null == val2){

​           return val2;

​        }else{

​           return bal2.trim();

​        }

​    }

}

 

HttpContext context

String parem = context.getHttpServletRequest().getParameter("xxx");

ObjectMapper mapper = new ObjectMapper();

StressTaskClass cc = mapper.readValue(parem,StressTaskClass.class);

 

===============================================================================JSON对象转化为Map===================================================================================

main{

​     final Map<String,String> result = new HashMap<String,String>();

​     JSONObject jsonObj = JSONObject.formObject(str2);

​     if(null == jsonObj){ return result;}

​     final Iterator iterator = jsonObj.keys();

​     String key = null;

​     String value = null;

​     while(iterator.hasNext()){

​         key = (String)iterator.next();

​         value = jsonObj.getString(key);

​         result.put(key,value);

​     }

​     return result;

}

 

===============================================================================JSON字符串转换为json对象===================================================================================

JSONObject resultJson = JSONObject.parseObject(esSql);

 

===============================================================================ORACLE decode函数===================================================================================

decode(value,if1,then1,if2,then2,......,else)

 

例子：取较小值

select decode(sign(变量1-变量2),-1,变量1,变量2) from dual;

 

sign()是根据某个值是0、正数、负数、分别返回 0、1、-1

 

应用：行转列

decode、sum、group by

select t.user_name , sum(decode(t.course,'语文'，score,null)) as CHINESE,

sum(decode(t.course,'数学'，score,null)) as MATH,

sum(decode(t.course,'英语'，score,null)) as ENGLISH

from test_tb t

group by t.user_name

 

 

表结构： tb_name(id,remark)

1  A

1  B

1  C

2  A

2  D

变成：

1  A,B,C

2  A,D

 

select a.id wm_concat(a.remark) rr from tb_name a group by a.id

 

 

 

 

===============================================================================Process===================================================================================

java可以通过Runtime调用系统命令，形式如下:  Runtime.getRuntime().exec(command); 这样执行没有任何输出，因为Runtime.getRuntime().exec(command) 将产生一个本地的进程，

并返回一个Process子类的实例，通过流来进行重定向。

 

===============================================================================文件操作===================================================================================

public class test(){

   /*

​      以字节为单位读取文件，常用于读取二进制文件，如 图片、声音、影像等文件

   */

   InputStream in;

   in.read();

   in.available(); //返回下一次对此输入流调用的方法可以不受阻塞的从此输入流读取的剩余字节数

 

   /*

​      随机读取文件

   */

   main(){

​       RandomAccessFile ranFile = new RandomAccessFile(fileName,"r");

​       //文件长度，字节数

​       long fileLength = ranFile.length();

​       //读文件的起始位置

​       int beginIndex = (fileLength > 4)?4:0;

​       //将读文件的初始位置移到beginIndex位置

​       ranFile.seek(beginIndex);

   }

   

   /*

​      读取一行特定长度的字符

   */

   int maxInputLength = 888;

   StringBuilder sb = new StringBuilder();

   int counts = 0;

   int m;

   while(true){

​      m = in.read();

​      if(m == -1){

​        if(sb.length() == 0){  return null;}

​        break;

​      }

​      if(m == '\n'){

​        break;

​      }

​      if(m == '\r'){

​        continue;

​      }

​      counts ++ ;

​      if(counts > maxInputLength){

​        xxxx

​      }

​      sb.append((char)m);

   }

   return sb.toString();

   

}

===============================================================================字符串换行===================================================================================

String str = "\r\nHello World";

sys.out(str);  //换一行

 

String str = "\r \nHello World";

sys.out(str);  //换2行

 

===============================================================================字节流和字符流===================================================================================

byte 与 Byte：

byte是基本数据类型

Byte是byte的包装类

 

字节 byte

位 bit

 

1字=2字节(1 word = 2 byte)

1字节=8位(1 byte = 8bit)

 

bps 是 bits per second 的简称

bit 电脑记忆体中最小的单位，在二进位电脑系统中，每一bit 可以代表0 或 1 的数位讯号。

Byte一个Byte由8 bits 所组成，可代表一个字元(A~Z)、数字(0~9)、或符号(,.?!%&+-*/)，

 

1 Byte = 8 Bits

1 KB = 1024 Bytes

1 MB = 1024 KB

1 GB = 1024 MB

 

程序中的输入输出都是以流的形式保存的，流中保存的都是字节

1个字符=2个字节，1个字节8bit，即8位2进制

在字节流中，输入用InputStream,输出用OutputStream，主要处理字节、字节数组或二进制对象，处理单元为1个字节，

在字符流中，输入用Reader,输出用Writer，主要处理字符、字符数组或字符串，处理单元为2个字节的Unicode字符。

字符流是java虚拟机将字符转化为2个字节的Unicode字符为单位的字符而成的，所以它对多国语言支持性比较好！

!!!!!!!!!!!!!!!!!!!!如果是中文文本的，用字符流较好，如果是音频文件、图片、歌曲用字节流好点。!!!!!!!!!!!!!!!!!!!!

所有文件的存储都是字节byte的存储，在磁盘上保存的不是文件的字符，而是先把字符编码成字节，再存储这些字节到磁盘，

在读取文件时，也是一个一个字节的读取以形成字节序列

字节流可作用于任何类型的对象，包括2进制对象，而字符流只能处理字符或者字符串。

字节流和字符流之间通过byte[]和String来关联。

 

public abstract class OutputStream extends Object implements Closeable,Flushable

Flushable表示刷新，清空内存中的数据

main：

   File f = new File("...//a.txt");

   OutputStream out = new FileOutputStream(f);

   String str = "Hello World"；

   byte[] b = str.getBytes(); //String编码为byte序列

   out.write(b); //因为是字节流，所以要转化成字节数组进行输出

   out.close();

以上输出只会覆盖，如果要追加的话，FileOutputStream另一个构造方法：

public FileOutputStream(File f,boolean append) append为true表示追加。

 

字节流转化为字符流：byte[] ===> String ：

byte[] b，String s = new String(b)  or  new String(b，String CharsetName)

字符流转化为字节流：String ===> byte[] ：

String s, byte[] b = s.getBytes()  or  s.getBytes(String CharsetName)

char[] ===> String ：

char[] c，String s = new String(c,0,len)

 

字符流的2个基类：Writer Reader，子对象：FileWriter FileReader BufferedWriter BufferedReader

字节流：byte[]  字符流：char[]、String

 

 

--------------************ 字节流在操作的时候本身是不会用到缓冲区的（内存），是与文件本身直接操作的，而字符流在操作的时候是用到缓冲区的，

字节流在操作文件时，即使不关闭资源（close），文件也能输出，但是如果字符流不使用close，就不会输出任何内容，说明字符流在操作的时候是用到缓冲区。并且可以强制使用flush方法

换个说法：

字节流，没有执行out.close()，文件中依然存在了要写的内容，说明字节流是直接操作文件的，字符流，没有执行out.close()，文件中不存在要写的内容，说明字节流不是直接操作文件的，

在关闭字符流时会强制将缓冲区的内容进行输出，即flush()。

 

在所有的硬盘上保存文件或进行传输的时候都是以字节的形式进行的，包括图片，而字符只有在内存才形成

FileWriter fw = new FileWriter("xxx");

BufferedWriter bw = new BufferedWriter(fw);

while(xx){

​    bw.write(xxx);

​    bw.newLine();

​    bw.flush(); //只要用到缓冲区就要记得刷新

}

bw.close();

 

close和flush的区别：flush后流可以继续使用，close后流就关闭了，close时就已经执行了刷新的操作。

 

NIO：

缓冲区Buffer、通道Channel、选择器Selector，IO时面向流的，NIO是面向缓冲区的

IO是阻塞的： 当一个线程调用了read write时，该线程被阻塞，直到有数据被读取、或数据被完全写入，该线程在此期间不能做任何事情

NIO是非阻塞模式：一个线程从通道发送请求读取数据，但它仅能得到目前可用的数据，如果目前没有数据可用，就什么都不会获取，而不是保持线程阻塞，所以

直至数据变的可以读取之前，该线程可以继续做其他的事情。

 

===============================================================================SQL 优化===================================================================================

使用DECODE函数可以避免重复扫描相同记录 或 重复连接相同的表：

SELECT COUNT(*)，SUM(SAL) FROM EMP WHERE DEPT_NO = 0020  AND ENAME LIKE　‘SMITH%’;

 

SELECT COUNT(*)，SUM(SAL)  FROMEMP  WHERE DEPT_NO = 0030  AND ENAME LIKE　‘SMITH%’;

 

你可以用DECODE函数高效地得到相同结果

 

SELECT COUNT(DECODE(DEPT_NO,0020,’X’,NULL)) D0020_COUNT,

 

COUNT(DECODE(DEPT_NO,0030,’X’,NULL)) D0030_COUNT,

 

SUM(DECODE(DEPT_NO,0020,SAL,NULL)) D0020_SAL,

 

SUM(DECODE(DEPT_NO,0030,SAL,NULL)) D0030_SAL

 

FROM EMP WHERE ENAME LIKE ‘SMITH%’;

 

类似的,DECODE函数也可以运用于GROUP BY 和ORDER BY子句中.

 

2.在含有子查询的SQL语句中，要注意减少对表的查询，update多个列：

例子：

update tb set id = (select max(xx) from tb2), name = (select max(yy) from tb2) where ss = 99;

改成：

update tb set (id,name) = (select max(xx),max(yy) from tb2) where ss = 99;

 

3.用where子句代替having子句

having只会在检索出所有记录之后才对结果集进行过滤，这个处理需要排序，总计等操作，如果能通过where子句限制记录的数目，就能减少这方面的开销

 

4.in exists

采用表连接的方式 比 in exists更有效率

例子：

select xx from tb1 where exists( select yy from tb2 where .....);

改成：

select xx from tb1,tb2 where ....

 

 

===============================================================================oracle 常用函数===================================================================================

select substrb('19920121',1,4) from dual;

----------------1992

 

select replace('xxerport','xx','se') from dual;

----------------seerport

 

select concat('xxerport','xx') from dual;

----------------xxerportxx

 

instr（'源字符串' , '目标字符串' ,'开始位置','第几次出现'）

select instr('oracle traning','ra',1,1) from dual;  ----------------   2

select instr('oracle traning','ra',1,2) from dual;  ----------------   9

 

ADD_MONTHS(data,n)

select ADD_MONTHS(SYSDATE,4) from dual; ----------------   2011-9-30

 

Last_day(date) 返回给定日期对应月份最后一天的时间

 

to_char 将一个数字或日期转换成字符串

select to_char(SYSDATE,'yyyy/mm/dd hh:mi:ss') from dual;  ----------------   2017/1/1 24:29:22

 

to_date 将字符串转换成日期类型

select to_date('20090808010203','yyyymmdd hh:mi:ss') from dual;  ----------------   2017-1-1 24:29:22

 

to_number 将字符串转换成数字

select to_number('1296') from dual;  ----------------   1296

 

abs()绝对值

nvl(w1,w2)

 

cell(n) 取大于等于N的最小整数

floor(n) 取小于等于N的最大整数

select floor(1.2) from dual;  ----------------   1

round(x[,y]) 返回四舍五入后的值,y不为整数则截取y整数部分，如果y>0四舍五入为y位小数，如果y<0四舍五入到小数点向左第y位

select round(555.6666,2),round(555.6666,-1),round(555.6666) from dual;  ---------------- 555.67 560 556

trunc()做截尾处理

select trunc(555.6666,2),round(555.6666,-1),round(555.6666) from dual;  ---------------- 555.66 550 555

 

over(partition by ) 效率没有 group by 高,但是提供了更多的功能

row_number over(partition by col1 order by col2) 表示根据col1分组，在分组内部根据col2排序，此函数计算的值表示每组内部排序后的排序编号：

 

 

分组排序取第一条,每个分组取第一个：

1.使用ROW_NUMBER() OVER(PARTITION BY COLUMN1 ORDER BY COLUMN2)先进行分组。

select a.CompanyID,a.UserID,a.AddTime,a.JF,

ROW_NUMBER() over(partition by a.CompanyID order by a.UserID) as new_index FROM dbo.LB_Company a

 

：

CompanyID  UserID  AddTime  JF  new_index

361         1        11     11     1

361         2        ss     xx     2

361         4        ss     xx     3

361         9        xx     yy     4

55         1        11     11     1

55         2        ss     xx     2

55         4        ss     xx     3

55         9        xx     yy     4

 

将上述结果作为一个表，外嵌查询select，使用条件new_index=1就可以查询出第个分组的第一条数据，从而达到去重的目的。

select * from(

select a.CompanyID,a.UserID,a.AddTime,a.JF,

ROW_NUMBER() over(partition by a.CompanyID order by a.UserID) as new_index FROM dbo.LB_Company a

)t where t.new_index=1

===============================================================================oracle 索引学习===================================================================================

rowid和rownum

rowid：数据库中一条记录的唯一地址，在该条数据创建时被确定下来，直接指向硬件上的存储位置。

rownum：伪列，主要作用是分页。

 

\1.  若没有索引，搜索某个记录时（例如查找name='wish'）需要搜索所有的记录，因为不能保证只有一个wish，必须全部搜索一遍

\2. 若在name上建立索引，oracle会对全表进行一次搜索，将每条记录的name值哪找升序排列，然后构建索引条目（name和rowid），

存储到索引段中，查询name为wish时即可直接查找对应地方

表数据和索引存放在数据块中，数据块是数据读写的最小单元，即使只需要读取一条数据，也会把整块的数据读到内存中，写数据也一样，

 

唯一索引：

create unique index xx on tb(yy)

 

select yy from tb; ------------index fast full scan: 可以并行访问索引，但输出不按顺序。

 

联合索引：不同值越少的列，越要放在前面。

 

表中的数据是无序的存放在数据库块中，数据在表中的顺序也不一定是录入的顺序。

如果想从表中查询某条数据，在没有索引时只能扫描表的所有的数据块，即 全表扫描；

与表的无序存放不同，索引是有序存放的，在存放索引的数据块上，数据都是有序的，并且数据块之间使用指针进行关联。

索引中保存的：索引的键值(索引列的值，表中那个列上有索引，且该列的实际值)，数据在表中的地址（rowid），就好比查字典按拼音目录查，

索引需要空间来存储，需要定期维护，每当有数据在表中增减，或索引列被修改时，索引会被动态的维护；

索引结构： 与表数据的不同，索引的数据块会组成一个树形结构，每个索引块包含N条数据，每条数据是一个key和value，这个value保存了一个

指针/地址，指向下一级的索引块或数据块。对于根节点和分支节点，它需要根据这个指针找到对应的子节点。

对于叶子节点，它需要根据这个指针找到对应的数据地址，它保存的就是rowid

在叶子节点中，每个数据块还会保存相邻叶子节点的地址。在每一层索引节点和每个索引块中，索引的键值都是有序的，默认升序。

索引中不包含空的键值，对于字典，不管拼音索引还是首部索引，保存的汉字是一样多的，但是Oracle索引不是这样的。

例如对于name的索引，如果某条数据的name为空，那么索引中就没有这条数据。

性能调优：数据库运行资源有3部分：IO、CPU、network。IO是把数据从磁盘读到内存的过程；CPU是处理的过程，network是网络传输的过程。逻辑读和物理读是影响性能的重要因素。

逻辑读是指要读的数据块已经在缓存中，不需要发生实际的IO。物理读是要把数据读到缓存中，需要发生实际的IO。读内存是读磁盘的速度的10倍，这就是同样的sql，第一次执行往往比第二次执行慢。

性能调优的根本方法是减少读取的数据块，对于索引扫描来说，读取的数据块包括定位到的叶子块，以及叶子块指向的表的数据块，这2部分。全表扫描支持多块读，即一次IO读多个数据块，可以减少IO的消耗，索引扫描一般是单块读，想想查字典的例子，为什么通过索引访问不能使用多块读。

执行计划：3方面考虑：访问路径、连接方式、连接顺序。访问路径包括全表扫描和索引扫描。

访问路径：

/*+full(a)*/ 是全表扫描     /*+index(a PK_T_USERINFO)*/ 是强制制定某个索引，PK_T_USERINFO是索引名，a是表的别名。

 

索引范围扫描：索引唯一扫描在叶子块中只能找到一条数据，索引范围扫描可能找到多条数据。

例如：userID=100，假设占用3个索引块，这3个索引块是相邻的叶子快。这里的相邻是指 指针关联的，不一定是

物理位置的连续，此时只需要扫描3个叶子块。但是注意：访问3个叶子块，只有第一次是从根节点下来的，后面的都是根据叶子块的指针来访问的，

很多初学者会以为每查一条数据都是从根节点开始扫描的

全模糊查询： userID like '%abc%'：这个查询不能使用userID的索引范围扫描。

查询列上有表达式或者函数 例如 userID || " = 'abc'，此时不能使用索引扫描的，这是常用的屏蔽索引的方法。

 

索引的选择：

有rownum的条件：例如查询id=1 and rownum<100，id上有索引，此时即使id=1有1万条数据，依然走id的索引范围扫描，因为只要查询到100条id=1的数据就终止了，不会继续扫描后面的叶子块。

组合索引： id=1 and type=1，能快速定位到目标叶子块，但是 id>1 and type=1就不行了，因为组合索引的键值是先按照第一个列排序的，当第一个列相同时才按照第二个列排序。例如有100w条数据满足

id>1 但是 type=1就只有一条，此刻可能访问了上万个叶子块。如果反过来 id=1 and type>1，有100w条数据满足id=1，type>1就只有一条，此时使用这个组合索引可以快速的定位到目标数据的第一个叶子块，

id=1，往后扫描时，只要出现第一个id不等于1 and type>1的数据，就可以终止了。

count(*) 要访问的数据都在索引里，可以不访问表。但大部分，例如 id=1 and type=12，根据id的索引查出30条满足id=1的数据，那么就需要根据rowid访问到表数据，才能判断type=12的条件是否成立。type=12不是用来定位位置的乐，只用于过滤数据了。

结论：当索引命中很多数据时，索引范围扫描开销大于全表扫描，一般查询超过5%的数据就不建议使用范围扫描了。

索引的选择性：索引列中不同值的数目与表中记录数的比，这个值越接近1，这个索引的效率就越高。确定索引的选择性：手工测量和自动测量。

手工测量：例如根据一个表的2列创建一个复合索引：

select count(distinct f1 || '%' || f2)/count(*) from tb,手工的优点是在创建索引之前就可以评估索引的选择性。

第二，也可以直接查询 USER_TAB_COLUMNS 这个表每个列的选择性。 select column_name,num_distinct from USER_TAB_COLUMNS where table_name = 'xxx'；表的选择性 = num_distinct/总行数。

 

索引设计规则：

1.数据量超过1000的表应该有索引。  

2.经常与其它表进行连接查询的表，在连接字段上应该有索引。这些字段主要是一些外键。  3.在where子句中常用的查询字段用索引

4.在经常需要根据范围进行搜索的列上 或 需要排序的列上 创建索引，因为索引已经排序了。  

5.查询字段是作为函数的参数出现时，可以对该字段创建函数索引，例如 UPPER(XXX) = 'XXX'

6.对于B+树索引，选择 选择性高的字段做索引。  7.不要在经常被修改的字段上建立索引。 8.列中有很多空值，不适合建立索引。  

9.复合索引要慎重，尽量选择单字段索引代替

10.复合索引的几个字段是否是经常同时以and的形式出现在 where子句中？单字段查询是否极少？ 如果是建议组合索引。

11.如果组合索引中包含的字段单独经常出现where子句中，则分解为多个单字段索引。

12.在索引列上使用计算 或在非基于函数索引列上使用函数 ：  where id+10 >20 ，此时使用索引不适合。

13.使用不等于 <> 、!= 不使用索引  14.使用了not ：  id not in (1,2,3,4)，此时使用索引不适合。  15.like左模糊查询，不使用索引

16.使用了|| 是 字符连接函数，不使用索引  where id || type = 'ddddd'

17.函数索引：  create index ss on tb(UPPER(ID))

18.比较不匹配的数据类型时：oracle会自己进行类型转换，相当于调用了函数，索引失效

select * from tb where id = 1234,若id是字符类型，则自动转换： select * from tb where to_number(id) = 1234,id索引失效。

 

索引全扫描一般效率低于全表扫描，但是有个特殊场景：当需要对一个大数据的表排序，然后返回TOP N时，可以使用索引全扫描来避免排序。因为排序需要把所有的数据读到内存中，非常消耗性能。

索引全扫描：select /*+index(a PK_T_USERINFO)*/

索引快速全扫描：可以使用多块读，也可以并行执行，执行结果不一定是有序的，因为索引快速全扫描oracle根据索引行在磁盘上的物理存储顺序来扫描，而不是根据索引树的指针顺序来扫描的，所以结果是无序的。

索引快速全扫描： select /*+index_ffs(a PK_T_USERINFO)*/ ,索引快速全扫描的应用条件： 只需要访问索引，不需要访问表。要访问的数据在索引中都存在。

 

索引跳跃扫描: 使用于组合索引第一个列没被用到 或 取值很少的情况： select /*+index_ss(a PK_T_USERINFO)*/

 

===============================================================================oracle 执行计划===================================================================================

执行计划是Oracle优化器在执行sql时选择的执行方案，虽然SQL语句中存在3个甚至更多的表连接，但是实际优化器每次只能做2个表的连接。

表之间的连接类型：  嵌套循环、哈希连接

嵌套循环：以驱动表（外表），先扫描该表，对该表的每一条数据全表扫描（内表），最有返回匹配的数据，这个过程像java的循环语句

 

假设A表是个大表，有4000万数据，占有100万个块，B是个小表，有4000数据，占有100个块

嵌套循环：

<1>以小表为驱动表 leading(b)：并不是大表就一定不能做驱动表，实际上只需要关联的数据集小就应该做驱动表。

select /*+use_nl(a b) full(a) full(b) leading(b)*/* from A a ,B b where a.num = b. num;

以B为驱动表（外表），先扫描该表，对该表的每一条数据全表扫描A（内表），最有返回匹配的数据，这个过程像java的循环语句

以小表为驱动表访问的数据块：4000*100W + 100 个块

以大表为驱动表访问的数据块：4000w*100 + 100w 个块，

所以以小表做驱动表好些。

 

<2>内表的关联列上必须要有索引

select /*+use_nl(a b) full(a) leading(b)*/* from A a ,B b where a.num = b. num;

此刻对B表的每一条数据去查A表时，使用的是内表的关联列上的索引，B查出来的数据到A表做索引范围扫描。

得到查询到目标数据的ROWID，再到A表中根据ROWID直接获得目标数据的信息。

假设索引的高度是4，最终有4000条数据命中：对B表全表扫描时需要访问100个块，B表每一条数据都扫描A的索引块一次，需要4000*4 = 1.6W个块，使用rowid到表需要访问4000个块，

表的数据也是放在块里面。A表一个rowid对应一条数据，也即对应一个块，所以是4000，总共访问的块： 100+1.6W+4000，比上面的方式性能更好。

 

<3>带有其他条件的嵌套循环：

当B表上有索引，且查询条件加上 and b.num = '123'时，使用哪个表做驱动表好？

select /*+use_nl(a b) full(b) leading(a)*/* from A a ,B b where a.num = b. num and a.num = '123';

虽然A表比B表大，但是A表应用条件a.num = '123'后只能查出1条数据，如果以A表做驱动表，需要访问B表的索引次数为1次，而反过来需要4000次，此时用A表做驱动表好

 

<4>带有子查询的嵌套循环

1.如果主查询的表需要连接的数据量小，且子查询的表的关联列上有索引，那么应该以主查询的表为驱动表：

select /*+full(b)*/* from B b where exists (select /*+no_unnest*/1 from A a where b.num = a.num;)

2.如果子查询的表需要连接的数据量小，应该以子查询的表为驱动表，

select /*+ordered use_nl(b) index(b pk_t_info)*/* from B b where exists (select /*+full(a)*/1 from A a where b.num = a.num;)

3.not in/not exists的子查询，只能以主查询为驱动表，一般尽量用 not exists,而不用 not in，因为只要有一条数据关联列的值为空，not in 的结果就是空

select /*+full(b)*/* from B b where not exists (select /*+no_unnest*/1 from A a where b.num = a.num;)

4.如果是外连接，那么只能以左表为驱动表，这一点在hash连接时也是如此。

即使指定A表为驱动表，优化器仍选择B为驱动表

select /*+use_nl(a b) leading(a)*/* from B b，A a where b.num = a. num(+); //实际运行结果仍是leading(b)

 

补： + 可以理解为 +表示补充，即哪个表有+，哪个表就为匹配表，该表是后来加上的，+号写在右表，左表就全部显示，顾为左连接。

 

<5>多表的嵌套循环

select /*+ordered use_nl(a b c) full(a) index(b pk_t_info) index(c pk_tc_info)*/* from A a,B b,C c where a.num = b.num and b.num = c.num

ordered指定表的连接顺序为a》b》c ， use_nl指定表的连接方式是嵌套循环,此时A表只能是全表扫描

多表连接时最重要的是连接顺序，一般原则是优先连接中间结果少的表。

例如a,b,c三个表的连接，最终结果是100条数据，如果a和b的连接结果是100w数据，再和C连接结果是100条数据，如果a和c的连接结果是200数据，再和b连接结果是100条数据，

显然a和c先连接比a和b先连接好。

 

嵌套循环使用场景：

《1》驱动表的结果集小（应用过自己的查询条件后）

《2》内表的连接列上有索引

《3》驱动表和内表连接匹配的数据量小，即扫描内表连接列的索引次数少。

 

 

哈希连接：

嵌套循环只适用于连接数据量小的情况，如果有上百万数据量要连接，可能需要对内表做上百万次索引范围扫描，导致内表的很多数据块被重复扫描，而且索引范围扫描如果扫描

超过5%的数据就比全表扫描的性能还差了。此时考虑hash连接。

select /*+leading(b) use_hash(a b) full(a) full(b)*/* from B b，A a where b.num = a. num;

1.选择一个表在内存中使用连接列生成hash表，这个表就是选择的驱动表，由于需要在内存中（PGA）生成hash表，所以选择数据集较少的表为驱动表较好。如果内存中放不下这个

hash表，那么就需要放到临时表空间中，如果临时表空间也满了，就会报错了。这个步骤需要全表扫描驱动表，不管另一个表有没有数据，即使使用了rownum条件，这个全表扫描也是必须做的

2.全表扫描探测表，查询hash表，当驱动表使用连接列生成了hash表后，遍历另一个表（也叫探测表），对探测表的每一条数据使用连接列的值到hash表中匹配，如果匹配上将数据保存到结果集中。

如果查询条件中有 rownum<=100的条件，那么只要找到100条满足的数据就可以停止探测表的扫描了。

3.hash连接结束就得到连接结果，跟索引扫描不同，hash连接一般不需要再访问表的，所以hash连接对表的扫描一般是全表扫描或快速全索引扫描。

 

带子查询的hash连接与嵌套循环类似，对in/exists的连接可以使用hash_sj提示，对not in/not exists的连接可以使用hash_aj提示

select /*+full(b)*/* from B b where exists (select /*+hash_sj full(a)*/1 from A a where b.num = a.num;)

select /*+full(b)*/* from B b where not exists (select /*+hash_aj full(a)*/1 from A a where b.num = a.num;)

 

update技巧：

如果需要使用b表的值更新a表对应的值，并且a和b都是大表，该怎么做呢？

由于a和b都是大表，需要大量的数据连接，显然应该使用hash连接，但是由于是update语句，下面这样是用不了hash连接的，实际还是嵌套循环

update /*+use_hash(b)*/* from B b set b.name =  (select /*+use_hash(a)*/1 from A a where b.num = a.num;)

应该这样做：PL/SQL程序块使用rowid更新

begin

   for item in (select/*+leading(a) use_hash(a b)*/a.rowid,b.info from A a, B b where a.id = b.id) loop

   update A set name = item.info where rowid = item.rowid;

   end loop;

end

 

使用并行查询：为了快速获得查询结果，对大表的查询可以设置并行查询。

select /*+leading(b) use_hash(a b) full(a) full(b) parallel(a,4) parallel(b,4)*/* from B b，A a where b.num = a. num(+);

hash连接使用场景：

《1》适用于较大数据集的连接，并且连接条件必须是等值连接。

《2》选择小的数据集作为驱动表在内存中生成hash表。

《3》设置一个较大的PGA可以加速hash的连接速度，避免使用临时表空间

《4》多表连接时同样注意连接顺序，中间结果集尽量小。

 

执行计划需要提示：

1.指定表的连接顺序，使用leading、ordered等，leading、ordered不能同时使用，ordered指定多个表的连接顺序。

2.指定表的连接方式，use_nl、use_hash

2.指定表的访问路径，full、index等

 

屏蔽索引：可以在列上可以追加一个表达式 例如： where a.num || " = 'XXX'

hash连接相对于嵌套循环，它实际上是通过空间换取时间，因为他需要保存hash表，在临时表空间不足时会报错，嵌套循环一般不会报错，但可能非常慢

===============================================================================数据库循环插入数据===================================================================================

begin

   for i in 1..222 loop

​     insert into tb values ();

   end loop;

   commit;

end;

 

===============================================================================创建一个Jetty应用服务===================================================================================

jetty.xml :

<? xml version="1.0" encoding="UTF-8" ?>

   <server>

​      <connectors host="10.134.118.73">

​         <connector name="default" port= "8810">

​             <arg name="maxIdleTime"> 30000 </arg>

​             <arg name="Acceptors"> 2 </arg>

​             <arg name="statsOn"> false </arg>

​             <arg name="confidentialPort"> 8810 </arg>

​             <arg name="lowResourcesConnections"> 5000 </arg>

​             <arg name="lowResourcesMaxIdle"> 5000 </arg>

​         </connector>

​         <base> webapp </base>

​         <welcomeFiles>

​             <welcomeFile file= "index.html">  

​             </welcomeFile>

​             <action sub-path = "/analysis.html" method= "queryAnalysis" />

​         </welcomeFiles>

​      </connectors>

​    </server>

 

import java.lang.reflect.Method;    

import java.net.InetAddress;

import java.net.NetWorkInterface;

import java.net.URL;    

import javax.servlet.http.HttpServletRequest;

import org.eclipse.jetty.server.Server;

import org.eclipse.jetty.server.handler.HandlerList;

import org.eclipse.jetty.server.handler.ResourceHandler;

import org.eclipse.jetty.server.nio.SelectChannelConnector;

import 自己的Rest

import 自己的DefaultHandler;

import 自己的HandleAction;

main:{

​    File f = new File(jetty.xml);

​    InputStream is = new FileInputStream(f);

​    Server server = new Server();

​    HandlerList handlers = new HandlerList();

​    SAXReader reader = new SAXReader();

​    //读配置文件

​    String host = xxx;

​    int port = xxx;

​    SelectChannelConnector connector = new SelectChannelConnector();

​    connector.setPort(port);

​    connector.setHost(host);

​    connector.setMaxldleTime(xx);

​    connector.setAcceptors(xx);

​    connector.setAcceptQueueSize(10);

​    connector.setStatsOn(false);

​    connector.setConfidentialPort(xxx);

​    connector.setLowResoucesConnections(500);

​    connector.setLowResoucesMaxldleTime(3000);

​    server.addConnector(connector);

 

​    //用于显示初始化页面，默认是index.xml

​    ResourceHandler resourceHandler = new ResourceHandler();

​    resourceHandler.setWelcomeFiles("index.html");

​    resourceHandler.setResourceBase("webapp");

​    

​    //用于注册REST

​    DefaultHandler handler = new DefaultHandler(port);

​    /*

​        <rest>

​           <class name = "xxx.DBSourceRest"></class>

​        </rest>

​    */

​    String name = "xxx.DBSourceRest";

​    List<Rest> restList = Rest.buildRest(name);

​    if(null != restList && restList.size() > 0){

​        for(Rest rest : restList){

​            handler.addRest(rest.getPath(),rest);

​        }

​    }

​    

​    handlers.addHandler(resourceHandler);

​    handlers.addHandler(handler);

​    handlers.addHandler(new org.eclipse.jetty.server.handler.DefaultHandler());

​    server.setHandler(handlers);

​    

​    //启动应用服务并等待请求

​    try{

​        server.start();

​        server.join();

​    }

}

​    

 

import javax.servlet.http.HttpServletRequest;

import javax.servlet.http.HttpServletResponse;

import net.sf.json.JSONObject;

import net.sf.json.JSONConfig;

import net.sf.json.util.CycleDetectionStrategy;

import org.eclipse.jetty.server.request;

import org.eclipse.jetty.server.handler.ContextHandler;

import 自己的Rest

public class DefaultHandler extends ContextHandler{

​    private static Comparator<String> comparator = new Comparator<String>(){

​         @Override

​         public int compare(String o1, String o2){

​             if(o1 == null || o2 == null){ return 0;}

​         }

​         return o2.compareToIgnoreCase(o1);

​    }

​    private Map<String,Rest> restMap = null;

​    

​    private int localPort = 0;

​    

​    public DefaultHandler(int port){

​        this.localPort = port;

​        this.restMap = new TreeMap<String,Rest>(comparator);

​    }

​    

​    @Override

​    public void doHandle(String target,Request baseRequest,HttpServletRequest request,HttpServletResponse response){

​        int port = baseRequest.getLocalPort();

​        if(port == localPort){

​             String key = target.toLowCase();

​             if(key != null && key.startsWith("/rest/")){

​                 String httpMethod = request.getMethod();

​                 String url = httpMethod + "@" + key;

​                 Rest rest = restMap.get(url.toLowCase());

​                 if(rest == null){

​                     super.doHandle(target,baseRequest,request,response);

​                     return;

​                 }else{

​                     baseRequest.setHandled(true);

​                     response.setStatus(HttpServletResponse.SC_OK);

​                     response.setContentType("application/json;charset=UTF-8");

​                     response.setCharacterEncoding("utf-8");

​                     response.setHeader("Cache-Control","no-cache");

​                     PrintWriter printer = response.getWriter();

​                     Object result = rest.handle(request);

​                     printer.println(new UIResult(result).toString());

​                     return;

​                 }

​             }

​        }

​        super.doHandle(target,baseRequest,request,response);

​    }

}

 

import net.sf.json.JSONArray;

import net.sf.json.JSONObject;

import net.sf.json.JSONConfig;

import net.sf.json.util.CycleDetectionStrategy;

public class UIResult{

​    private int status = 0;

​    private String message;

​    private Object data;

​    

​    //

​    getter() setter() 构造函数

​    

​    @Override

​    public String toString(){

​        String dataText = "";

​        if(null == data){dataText = "";}

​        else{

​           if(isSimpleType(data)){

​               dataText = String.valueOf(data);

​           }else if(data instanceof List){

​               JSONConfig jsonConfig = new JSONConfig();

​               jsonConfig.setCycleDetectionStrategy(CycleDetectionStrategy.LENIENT);

​               JSONArray jsonMembers = JSONArray.formObject(data,jsonConfig);

​               dataText = jsonMembers.toString();

​           }else{

​               JSONConfig jsonConfig = new JSONConfig();

​               jsonConfig.setCycleDetectionStrategy(CycleDetectionStrategy.LENIENT);

​               JSONObject jsonMembers = JSONObject.formObject(data,jsonConfig);

​               dataText = jsonMembers.toString();

​           }

​        }

​        return dataText;

​    }

​    

​    private boolean isSimpleType(Object val){

​        if(val.getClass() == Byte.class || val.getClass() == byte.class){ return true;}

​        if(val.getClass() == Boolean.class || val.getClass() == boolean.class){ return true;}

​        if(val.getClass() == Integer.class || val.getClass() == int.class){ return true;}

​        if(val.getClass() == Long.class || val.getClass() == long.class){ return true;}

​        if(val.getClass() == Float.class || val.getClass() == float.class){ return true;}

​        if(val.getClass() == Short.class || val.getClass() == short.class){ return true;}

​        if(val.getClass() == Double.class || val.getClass() == double.class){ return true;}

​        if(val.getClass() == String.class){ return true;}

​        return false;

​    }

 

 

}

 

 

 

 

===============================================================================Https服务器与调用端===================================================================================

启用Http服务器是写在rest后台响应里，先创建一个应用服务监听8810端口，在这个服务里注册rest

 

服务器端：

MyHttpsServer server = new MyHttpsServer();

server.init();

 

config.ini:

server.port=8443

server.context=/Http/GetHttpInfo

server.password = Huawei123

server.keystore = keystore

server.keystorePass = Huawei123

 

代码：

import java.net.InetSocketAddress;

import java.security.KeyStore;

import javax.net.ssl.KeyManagerFactory;

import javax.net.ssl.SSLContext;

import org.apache.commons.configuration.PropertiesConfiguration;

import org.apache.commons.configuration.reloading.FileChangeReloadingStrategy;

import com.sun.net.httpserver.HttpsConfigurator;

import com.sun.net.httpserver.HttpsServer;

import com.sun.net.httpserver.spi.HttpServerProvider;

 

public class MyHttpsServer{

   private HttpsServer server;

   public void init(){

​      init(null);

   }

   public void init(String localAddress){

​      PropertiesConfiguration config = new PropertiesConfiguration(new File("文件路径","config.ini"));

​      config.setReloadingStrategy(new FileChangeReloadingStrategy();   //动态更新

​      

​      int port = config.getInt("server.port");   //"8443"

​      String context = config.getString("server.context");   //"/Http/GetHttpInfo"   

​      String keystore = "文件路径" + File.separator + config.getString("server.keystore");  //要带上文件路径!! 是个文件，要找下 @2。服务器端的配置文件要看下  3.MyHttpsHandler需要导入的包

​      String keystorePass = config.getString("server.keystorePass");

​      

​      HttpServerProvider provider = HttpServerProvider.provider();

​      InetSocketAddress address;

​      if(null == localAddress){

​          address = new InetSocketAddress(port);

​      }else{

​          address = new InetSocketAddress(localAddress,port);

​      }

​      

​      //监听端口能同时接受100个请求

​      this.server = provider.createHttpsServer(address,100);

​      //https配置

​      HttpsConfigurator configurator = configHttps(keystore,keystorePass);

​      server.setHttpsConfigurator(configurator);

​      server.createContext(context,new MyHttpsHandler(config));

​      

​      //设置成null是使用单线程

​      //server.setExecutor(null);

​      server.setExecutor(Executors.newCachedThreadPool());

​      server.start();

   }

   

   private HttpsConfigurator configHttps(String keystore,String keystorePass){

​      //加载keystore文件

​      KeyStore ks = KeyStore.getInstance("JKS");

​      ks.load(new FileInputStream(keystore),keystorePass.toCharArray());

​      

​      KeyManagerFactory kmf = KeyManagerFactory.getInstance("SunX509");

​      kmf.init(ks,keystorePass.toCharArray());

​      

​      SSLContext sslContext = SSLContext.getInstance("TLS");

​      sslContext.init(kmf.getKeyManagers(),null,null);

​      

​      HttpsConfigurator conf = new HttpsConfigurator(sslContext);

​      return conf;

   }

   

   public void stop(){

​      if(null != server){

​         server.stop(1);

​      }

   }

}

 

import com.sun.net.httpserver.HttpExchange;

import com.sun.net.httpserver.HttpHandler;

public class MyHttpsHandler implements HttpHandler{

​    private final PropertiesConfiguration config;

​    private String passeord = "";

​    public MyHttpsHandler(PropertiesConfiguration config){

​      this.config = config;

​      this.passeord = config.getString("server.password");

​    }

​    

​    @Override

​    public void handle(HttpExchange httpExchange){

​      //处理网管发来的请求,requestBody为请求的xml

​      InputStream in = httpExchange.getRequestBody();

​      String requestBody = IOUtils.toString(in);

​      

​      String responseXml = parseRequest(requestBody);

​      byte[] bs = responseXml.getBytes("UTF-8");

​      httpExchange.sendResponseHeaders(200,bs.length);

​      

​      OutputStream out = httpExchange.getResponseBody();

​      IOUtils.write(responseXml,out);

​      

​      IOUtils.closeQuietly(in);

​      IOUtils.closeQuietly(out);

​    }

​    

​    public String parseRequest(String xmlDoc){

​      StringReader read = new StringReader(xmlDoc);

​      InputSource source = new InputSource(read);

​      SAXBuilder sb = new SAXBuilder();

​      Document doc = sb.build(source);

​      Element ele = doc.getRootElement();

​      ........

​    }

}

 

String keystore = "文件路径" + File.separator + config.getString("server.keystore");  //要带上文件路径!! 是个文件，要找下 @2。服务器端的配置文件要看下  3.MyHttpsHandler需要导入的包

keystore是个文件：这个文件在startup脚本生成,在jar包main方法执行之前，是证书库，里面包含私钥,此处是单向认证，只需要一段有证书。如果是双向呢？单向就是只是网管请求模拟桩，模拟桩不请求网管

startup.dat :

@echo off

set CURRENT_DIR = %~dp0

for /f "delims == tokens = 1,2" %%i in (%CURRENT_DIR%\config\config.ini)

do(

  if %%i == server.keystore set keystore = %%j

  if %%i == server.keystorePass set keystorePass = %%j

)

if exist %CURRENT_DIR%\config\%keystore%(

   del "%CURRENT_DIR%\config\%keystore%"

)

keytool -genkeypair -alias 1 -keypass "%keystorePass%" -storepass "%keystorePass%" -keystore "%CURRENT_DIR%\config\%keystore%" -dname "C=CN,ST=SX,L=SZ,O=IVS,OU=IVS" -keyalg RSA -keysize 2048 -validity 365

java -jar xxx.jar

 

startup.sh :

\#!/bin/bash

cd config

\#keystore = keystore

\#storepass = storepass

keystore = `grep  server.keystore = config.ini|awk -F '=' '{print $2}'`

storepass = `grep  server.keystorePass = config.ini|awk -F '=' '{print $2}'`

 

rm "$keystore"

keytool -genkeypair -alias 1 -keypass "$kstorePass%" -storepass "$storePass%" -keystore "$keystore" -dname "C=CN,ST=SX,L=SZ,O=IVS,OU=IVS" -keyalg RSA -keysize 2048 -validity 365

cd ..

JVM_OPT = "-Xdebug -agentlib:jdwp=transport=dt_socket,address = 8812,server = y,suspend = n"

java $JVM_OPT -jar xxx.jar &

 

http://www.importnew.com/21125.html

 

网管调用端：

String responseXml = sendRequest(requestXml);

Document doc = parseResponse(responseXml);

 

private String sendRequest(String requestXml){

   String url = PropertiesManager.getInstance.getUrl(); //https:// ip + port + serviceName 与服务端配的一样

   tring responseXml = HttpClientAdapter.doPostSync(url,requestXml);

   return responseXml;

}

 

import org.apache.commons.lang.StringUtils;

import org.jdom.Document;

import org.jdom.Element;

import org.jdom.input.SAXBuilder;

import org.jdom.output.Format;

import org.jdom.output.XMLOutputter;

import org.xml.sax.EntityResolver;

import org.xml.sax.InputSource;

import org.xml.sax.SAXException;

import org.xml.sax.EntityResolver;

public Document parseResponse(String xmlDoc){

   if(StringUtils.isBlank(xmlDoc)){

​      return;

   }

   xmlDoc = xmlDoc.replaceAll("&","&amp;");

   xmlDoc = xmlDoc.replaceAll("xml","x");

   Reader read = new StringReader(xmlDoc);

   SAXBuilder sb = new SAXBuilder();

   sb.setFeature("[http://apache.org/xml/features/disallow-doctype-decl",ture);](http://apache.org/xml/features/disallow-doctype-decl)

   sb.setEntityResolver(new EntityResolver()

   {

​                String emptyDtd = "";

​                

​                ByteArrayInputStream bytels = new ByteArrayInputStream(emptyDtd.getBytes("UTF-8"));

​                

​                /**

​                 \* {@inheritDoc}

​                 */

​                @Override

​                public InputSource resolveEntity(String publicId, String systemId)

​                    throws SAXException, IOException

​                {

​                    return new InputSource(bytels);

​                }

​    });

​    Document doc = sb.build(in);

​    return doc;

}

 

import java.text.Normalizer;

import java.text.Normalizer.Form;

import org.apache.commons.httpclient.HttpClient;

import org.apache.commons.httpclient.HttpConnectionManager;

import org.apache.commons.httpclient.HttpException;

import org.apache.commons.httpclient.methods.PostMethod;

import org.apache.commons.httpclient.params.HttpConnectionManagerParams;

import [org.apache.commons.lang.StringUtils](http://org.apache.commons.lang.stringutils/)

import org.eclipse.jetty.util.URIUtil;

public final class HttpClientAdapter{

​    private static final long  CONN_MAX_BUFFER_SIZE = 31457280L；

​    private static HttpClientManager httpClientManager = HttpClientManager.getInstance();

​    

​    public static String doPostSync(String url, String sendData)

​    {

​        String resultData = null;

​        int repCode = 0;

​        HttpClient httpClient = null;

​        if(!checkParam(url,sendData)){

​            return null;

​        }

​        try

​        {

​            httpClient = httpClientManager.getDefaultHttpClient();

​        }

​        catch (OMSException e1)

​        {

​            LOGGER.error("getDefaultHttpClient failed.e1=", e1);

​            return resultData;

​        }

​        PostMethod post = httpClientManager.getHttpPost(url, sendData);

​        httpClient.getHttpConnectionManager().getParams().setConnectionTimeout(15000);

​        httpClient.getHttpConnectionManager().getParams().setSoTimeout(300000);

​        try

​        {

​            repCode = httpClient.executeMethod(post);

​        }

​        catch (HttpException e)

​        {

​            LOGGER.error("executeMethod HttpException,e=", e);

​            return resultData;

​        }

​        catch (IOException e)

​        {

​            LOGGER.error("executeMethod IOException,e=", e);

​            return resultData;

​        }

​        

​        if (repCode == 200)

​        {

​            resultData = httpClientManager.getResponseMsg(post);

​        }

​        else

​        {

​            LOGGER.error("omu response error");

​        }

​        

​        return resultData;

​    }

​    

​    private boolean checkParam(String hostAddress,String sendData){

​        String normalAddr = Normalizer.normalize(hostAddress,Normalizer.Form.NFKC);

​        normalAddr = URIUtil.canonicalPath(normalAddr);

​        if(StringUtils.isEmpty(normalAddr) || !(normalAddr.startWith("http")) || sendData.isEmpty() || (sendData.length == 0)){

​           return false;

​        }

​        byte[] size = sendData.getBytes("UTF-8");

​        if(size > 31457280L){

​           return false;

​        }

​        return true;

​    }

}

 

import java.io.IOException;

import java.io.UnsupportedEncodingException;

import org.apache.commons.httpclient.HttpClient;

import org.apache.commons.httpclient.methods.PostMethod;

import org.apache.commons.httpclient.protocol.Protocol;

public class HttpClientManager

{

​    /**

​     \* HTTPS

​     */

​    public static final String HTTPS = "https";

​    

​    /**

​     \* HttpClient管理器单例

​     */

​    private static HttpClientManager instance = null;

​    

​    /**

​     *

​     \* 构造方法说明

​     *

​     \* @see 相关类或方法

​     */

​    public HttpClientManager()

​    {

​        LOGGER.info("HttpClientManager Constructors");

​    }

​    

​    /**

​     \* 获取单例。

​     *

​     \* @return HttpClientManager 单例

​     \* @see [类、类#方法、类#成员]

​     */

​    public static synchronized HttpClientManager getInstance()

​    {

​        if (null == instance)

​        {

​            instance = new HttpClientManager();

​        }

​        

​        return instance;

​    }

​    

​    /**

​     \* 实例化一个HttpClient

​     \* @return HttpClient

​     \* @throws OMSException OMSException

​     */

​    @SuppressWarnings("deprecation")

​    public HttpClient getDefaultHttpClient()

​        throws OMSException

​    {

​        int httpsPort = Integer.parseInt(PropertiesMgr.getInstance().getPort());

​        Protocol httpsProtocol = new Protocol("https", new IVSSecureProtocolSocketFactory(), httpsPort);

​        Protocol.registerProtocol("https", httpsProtocol);

​        HttpClient httpsClient = new HttpClient();

​        LOGGER.debug("init https client : {}", httpsClient);

​        return httpsClient;

​    }

​    

​    /**

​     \* 封装post请求

​     *

​     \* @param url

​     \*            连接地址

​     \* @param sendData

​     \*            发送数据

​     \* @return PostMethod

​     \* @author y00208965

​     \* @since eSightUCC V100R001C01

​     */

​    @SuppressWarnings("deprecation")

​    public PostMethod getHttpPost(String url, String sendData)

​    {

​        PostMethod post = new PostMethod(url);

​        // 设置数据格式和编码

​        post.addRequestHeader("Content-Type", "text/xml;Charset=UTF-8");

​        post.setRequestBody(sendData);

​        return post;

​    }

​    

​    /**

​     \* 获取响应

​     *

​     \* @param postMethod

​     \*            PostMethod

​     \* @return String

​     \* @author y00208965

​     \* @since eSightUCC V100R001C01

​     */

​    public String getResponseMsg(PostMethod postMethod)

​    {

​        LOGGER.debug("getResponseMsg: {}", postMethod);

​        String res = null;

​        try

​        {

​            byte[] body = postMethod.getResponseBody();

​            res = new String(body, "utf-8");

​            LOGGER.debug("resultData = {}", res);

​        }

​        catch (UnsupportedEncodingException e)

​        {

​            LOGGER.error("UnsupportedEncodingException,E=", e);

​        }

​        catch (IOException e)

​        {

​            LOGGER.error("IOException,E=", e);

​        }

​        finally

​        {

​            postMethod.releaseConnection();

​        }

​        

​        return res;

​    }

}

 

import java.net.InetAddress;

import java.net.InetSocketAddress;

import java.net.Socket;

import java.net.SocketAdress;

import java.security.cert.X509Certificate;

import java.net.SocketFactory;

import java.net.ssl.SSLContext;

import java.net.ssl.SSLSocketFactory;

import java.net.ssl.TrustManager;

import java.net.ssl.X509TrustManager;

import org.apache.commons.httpclient.params.HttpConnectionParams;

import org.apache.commons.httpclient.protocol.SecureProtocolSocketFactory;

import org.apache.commons.io.IOUtils;

public class IVSSecureProtocolSocketFactory implements SecureProtocolSocketFactory{

​    private SSLContext sslContext = null;

​    public Socket createSocket(Socket socket,String host,int port,boolean autoClose){

​        return getSSLContext().getSocketFactory().createSocket(socket,host,port,autoClose);

​    }

​    public Socket createSocket(String host,int port){

​        return getSSLContext().getSocketFactory().createSocket(host,port);

​    }

​    public Socket createSocket(String host,int port,InetAddress localAddress,int localPort,HttpConnectionParams params){

​        if(params == null){ throw exception};

​        int timeout = params.getConnectionTimeOut();

​        SocketFactory socketFactory = getSSLContext().getSocketFactory();

​        if(timeout != 0){

​           Socket socket = socketFactory.createSocket();

​           SocketAdress localaddr = new InetSocketAddress(localAddress,localPort);

​           SocketAdress remoteaddr = new InetSocketAddress(host,port);

​           socket.bind(localaddr);

​           socket.connect(remoteaddr,timeout);

​           return socket;

​        }

​        return socketFactory.createSocket(host,port,localAddress,localPort);

​    }

​    public Socket createSocket(String host,int port,InetAddress clientHost,int localPort){

​        return getSSLContext().getSocketFactory().createSocket(host,port,clientHost,localPort);

​    }

​    private SSLContext createSSLContext(){

​        this.sslContext = SSLContext.getInstance("SSL");

​        this.sslContext.init(null,new TrustManager[]{new TrustAnyTrustManager(null)},new SecureRandom());

​        return this.sslContext;

​    }

​    private SSLContext getSSLContext(){

​        if(null == sslContext){

​            this.sslContext = createSSLContext();

​        }

​        return this.sslContext;

​    }

​    private static class TrustAnyTrustManager implements X509TrustManager(){

​        public X509Certificate[] getAcceptedlssuers{

​            return new X509Certificate[0];

​        }

​    }

}

 

===============================================================================https服务器端 优化===================================================================================

import org.eclipse.jetty.server.Connector;

import org.eclipse.jetty.server.Server;

import org.eclipse.jetty.server.ssl.SslSelectChannelConnector;

import org.eclipse.jetty.server.ssl.SslContextFactory;

 

public class NewHttpsServer{

​     private Server server;

​    

​     private ServerJoinThread joinThread;

​    

​     public void start(String host){

​         this.server = new Server();

​         SslSelectChannelConnector ssl_connector = new SslSelectChannelConnector();

​         int port = config.getInt("server.port");   //"8443"

​         String context = config.getString("server.context");   //"/Http/GetHttpInfo"   

​         String keystore = "文件路径" + File.separator + config.getString("server.keystore");  //要带上文件路径!! 是个文件，要找下 @2。服务器端的配置文件要看下  3.MyHttpsHandler需要导入的包

​         String keystorePass = config.getString("server.keystorePass");

​        

​         ssl_connector.setHost(host); //模拟桩的IP

​         ssl_connector.setPort(port);

​         ssl_connector.setMaxldleTime(3000);

​         ssl_connector.setAcceptors(2);

​         ssl_connector.setAcceptQueueSize(10);

​         ssl_connector.setStatsOn(false);

​         ssl_connector.setLowResoucesConnections(500);

​         ssl_connector.setLowResoucesMaxldleTime(3000);

​         SslContextFactory cf = ssl_connector.getSslContextFactory();

​         cf.setKeyStorePath =(keystore);

​         cf.setKeyStorePassWord =(keystorePass);

​         cf.setKeyManagerPassword(keystorePass);

​         server.setConnectors(new Connector[]{ssl_connector});

​         server.setHandler(new NewHttpsHandler(config));

​        

​         //启动应用服务并等待请求

​         server.start();

​         this.joinThread = new ServerJoinThread(server);

​         this.joinThread.start();

​     }

​    

​     public void stop(){

​         server.stop();

​         this.joinThread.interrupt();

​         this.joinThread = null;

​     }

​    

​     class ServerJoinThread extends Thread{

​         private Server server;

​         public ServerJoinThread(Server server){

​             this.server = server;

​         }

​         @Override

​         public void run(){

​              this.server.join();

​         }

​     }

}

 

import javax.servlet.http.HttpServletRequest;

import javax.servlet.http.HttpServletResponse;

import org.eclipse.jetty.server.Request;

import org.eclipse.jetty.server.handler.AbstractHandler;

public class NewHttpsHandler extends AbstractHandler{

​     private String contextPath;

​     private NewRequestHandler requestHandler;

​     public NewHttpsHandler(PropertiesConfiguration config){

​          super();

​          this.contextPath = config.getxxx(); //   /Http/GetHttpInfo

​          this.requestHandler = new NewRequestHandler(config);

​     }

​     public void handle(String target,Request baseRequest,HttpServletRequest request,HttpServletResponse response){

​          if(target != null && target.startsWith(contextPath)){

​               response.setContentType("text/html;charset=utf-8");

​               response.setStatus(HttpServletResponse.SC_OK);

​               baseRequest.setHandled(true);

​               requestHandler.handle(request,response);

​          }

​     }

}

 

public class NewRequestHandler{

​    private final PropertiesConfiguration config;

​    private String passeord = "";

​    public NewRequestHandler(PropertiesConfiguration config){

​      this.config = config;

​      this.passeord = config.getString("server.password");

​    }

 

​    public void handle(HttpServletRequest request,HttpServletResponse response){

​      //处理网管发来的请求,requestBody为请求的xml

​      InputStream in = request.getInputStream();

​      String requestBody = IOUtils.toString(in);

​      String responseXml = xxx(requestBody);

 

​      response.setStatus(200);

​      response.getWriter().print(responseXml);

​      

​      IOUtils.closeQuietly(in);

​      IOUtils.closeQuietly(out);

​    }

​    

​    public String parseRequest(String xmlDoc){

​      StringReader read = new StringReader(xmlDoc);

​      InputSource source = new InputSource(read);

​      SAXBuilder sb = new SAXBuilder();

​      Document doc = sb.build(source);

​      Element ele = doc.getRootElement();

​      ........

​    }

}

 

 

config：

server.port = 8443

server.context = /Http/GetHttpInfo

 

===============================================================================HttpsURLConnection===================================================================================

import java.net.URL;

import javax.net.ssl.HttpsURLConnection;

import javax.net.ssl.SSLContext;

import javax.net.ssl.TrustManager;

 

public class HttpsUtil{

​    public static HttpsURLConnection connection = null;

​    public static SSLContext sc = null;

​    

​    public static void init(){

​        sc = SSLContext.getInstance("TLSv1.1");

​        sc.init(null,new TrustManager[]{new TrustAnyTrustManager()},new java.security.SecureRandom());

​    }

​    

​    //POST请求

​    public static void httpsAction(String url,String content){

​        if(sc == null){ return;}

​        URL realUrl = new URL(url);

​        connection = (HttpsURLConnection)realUrl.openConnection();

​        connection.setSSLSocketFactory(sc.getSocketFactory()); //设置证书认证

​        connection.setHostnameVerifier(new TrustAnyHostnameVerifier());

​        connection.setDoOutput(true);

​        connection.setDoInput(true);

​        connection.setRequestMethod("PUT");

​        connection.setRequestProperty("accept","*/*");

​        connection.setRequestProperty("connection","Keep-Alive");

​        connection.setRequestProperty("user-agent","Mozilla/4.0(compatible;MSIE 5.0;Windows NT;DigExt)");

​        connection.setRequestProperty("Content-Type","application/json;charset=UTF-8");

​        

​        OutputStream out = connection.getOutputStream();

​        out.write(content.getBytes("utf-8"));

​        out.close();

​    }

​    

​    //GET请求

​    public static void httpsGet(String url){

​        if(sc == null){ return;}

​        URL realUrl = new URL(url);

​        connection = (HttpsURLConnection)realUrl.openConnection();

​        connection.setSSLSocketFactory(sc.getSocketFactory()); //设置证书认证

​        connection.setHostnameVerifier(new TrustAnyHostnameVerifier());

​        connection.setDoOutput(true);

​        connection.setRequestProperty("accept","*/*");

​        connection.setRequestProperty("connection","Keep-Alive");

​        connection.setRequestProperty("user-agent","Mozilla/4.0(compatible;MSIE 6.0;Windows NT 5.1;SV1)");

​        connection.connect();

​    }

​    

​    public static String execute(){

​        String result = "";

​        InputStream is = null;

​        BufferedReader in = null;

​        if(connection == null || sc == null){

​            return result;

​        }

​        if(connection.getResponseCode() == 200){

​             is = connection.getInputStream();

​             //定义BufferedReader输入流来读取URL的响应

​             in = new BufferedReader(new InputStream(is));

​             String line;

​             while((line = in.readLine()) != null){

​                 result += line;

​             }

​        }else{

​             is = connection.getErrorStream();

​        }

​        return result;

​    }

​    

​    public static int httpsPut(String url,String content){

​        HttpsUtil.init();

​        HttpsUtil.httpsAction(url,content);

​        String re = HttpsUtil.execute();

​        if(re.contains("\"code\":0")){ return 0;}

​        if(re.contains("\"code\":\"1\"")){ return 1;}

​        return -1;

​    }

​    

​    TrustAnyTrustManager implements X509TrustManager

 

}

 

main:

HttpsUtil.httpsPut(url,XXX);

 

===============================================================================自己的rest===================================================================================

import java.lang.annotation.ElementType;

import java.lang.annotation.Retention;

import java.lang.annotation.RetentionPolicy;

import java.lang.annotation.Target;

 

@Retention(value = RetentionPolicy.RUNTIME)

@Target(ElementType.METHOD)

public @interface Del{}

 

@Retention(value = RetentionPolicy.RUNTIME)

@Target(ElementType.METHOD)

public @interface Get{}

 

@Retention(value = RetentionPolicy.RUNTIME)

@Target(ElementType.METHOD)

public @interface Post{}

 

@Retention(value = RetentionPolicy.RUNTIME)

@Target(ElementType.METHOD)

public @interface Put{}

 

@Retention(value = RetentionPolicy.RUNTIME)

@Target(ElementType.METHOD)

public @interface Path{

​    String value();

}

 

例子：

@Path("ivs/simulator/cluster")

public class ClusterRest{

  @GET

  @Path("init")

  public void test(){}

}

 

public class Rest

{

   private Object restObj;

   

   private String path;

   

   private Method method;

   

   public Object handle(HttpServletRequest request){

​       Class<?>[] paramTypes = method.getParameterTypes();

​       Object[] paramObjs = new Object[paramTypes.length];

​       int i = 0;

​       for(Class<?> cls: paramTypes){

​           if(cls == HttpServletRequest.class){

​               paramObjs[i++] = request;

​           }else{

​               paramObjs[i++] = null;

​           }

​       }

​       return method.invoke(restObj,paramObjs);

   }

   

   public static List<Rest> bulidRest(String name){

​       Object obj = Class.forName(name).newInstance();

​       Path clsPath = obj.getClass().getAnnotation(Path.class);

​       String clsPathVal = clsPath.value();

​       Method[] methods = obj.getClass().getDeclaredMethods();

​       List<Rest> restList = new ArrayList<Rest>;

​       for(Method m : methods){

​          String method = "";

​          if(m.getAnnotation(Get.class) != null){

​             method = "get";

​          }else if(m.getAnnotation(Post.class) != null){

​             method = "post";

​          }else if(m.getAnnotation(Del.class) != null){

​             method = "delete";

​          }else if(m.getAnnotation(Put.class) != null){

​             method = "put";

​          }else{

​             continue;

​          }

​          Path mPath = m.getAnnotation(Path.class);

​          String mPathVal = null;

​          if(mPath != null){

​             mPathVal = mPath.value();

​          }

​          String url = method + "@" + "/rest"

​          if(clsPathVal.startWith("/")){

​              url += clsPathVal;

​          }else{

​              url += "/" + clsPathVal;

​          }

​          if(mPathVal != null){

​              if(mPathVal.startWith("/")){

​                  url += mPathVal;

​              }

​              else{

​                  url += "/" + mPathVal;

​              }

​          }

​          Rest rest = new Rest();

​          rest.setPath(url.toLowCase());

​          rest.setRestObj(obj);

​          rest.setMethod(m);

​          restList.add(rest);

​          

​       }

​      return restList;

   }

   public void setPath(){}

   public void setRestObj(){}

   public void setMethod(){}

}

 

===============================================================================Oracle定时任务===================================================================================

Oracle job有定时执行的功能，可以在指定的时间点或每天的某个时间点自行执行任务。

重要的字段就是job这个值就是我们操作job的id号，what 操作存储过程的名称，next_date 执行的时间，interval执行间隔

执行间隔interval运行频率：

描述                              INTERVAL参数值

每天午夜12点                 TRUNC(SYSDATE + 1)

每天早上8点30分             TRUNC(SYSDATE + 1) +（8*60+30）/(24*60)

每星期二中午12点            NEXT_DAY(TRUNC(SYSDATE ),''TUESDAY'' ) + 12/24

每个月第一天的午夜12点        TRUNC(LAST_DAY(SYSDATE ) + 1)

每个季度最后一天的晚上11点     TRUNC(ADD_MONTHS(SYSDATE + 2/24, 3 ), 'Q') -1/24

每星期六和日早上6点10分        TRUNC(LEAST(NEXT_DAY(SYSDATE,''SATURDAY"), NEXT_DAY(SYSDATE, "SUNDAY"))) + （6×60+10）/（24×60）

 

每分钟执行

Interval =>TRUNC(sysdate,'mi') + 1/ (24*60)

如果改成TRUNC(sysdate,'mi')+ 10/ (24*60) 就是每10分钟执行次

 

每天定时执行

​       例如：每天的凌晨1点执行

​                    Interval =>TRUNC(sysdate) + 1 +1/ (24)

每周定时执行

​          例如：每周一凌晨1点执行

​           Interval =>TRUNC(next_day(sysdate,'星期一'))+1/24

每月定时执行

​          例如：每月1日凌晨1点执行

​           Interval=>TRUNC(LAST_DAY(SYSDATE))+1+1/24

 

/* 每10秒钟执行一次 插入一条时间 */：

1.

-- 创建table

create table A8

(

  a1 VARCHAR2(500)

)

\2.    

create or replace procedure proc_add_test as

begin

  insert into a8 values (to_char(sysdate, 'yyyy-mm-dd hh:mi'));/*向测试表插入数据*/

  commit;

end;

\3.    

declare

  job number;

BEGIN

  DBMS_JOB.SUBMIT(  

​        JOB => job,  /*自动生成JOB_ID*/  

​        WHAT => 'proc_add_test;',  /*需要执行的存储过程名称或SQL语句*/  

​        NEXT_DATE => sysdate+3/(24*60),  /*初次执行时间-下一个3分钟*/  

​        INTERVAL => 'trunc(sysdate,''mi'')+1/(24*60)' /*每隔1分钟执行一次*/

​      );  

  commit;

end;

 

 

1.可以通过查询系统表查看该job信息： select * from user_jobs；

2.手动sql调用job ：

begin

   DBMS_JOB.RUN(40); /*40 job的id*/

end;

3.删除任务

begin

  /*删除自动执行的job*/

  dbms_job.remove(40);

end;

4.停止job

dbms.broken(job，broken，nextdate);   

dbms_job.broken(v_job,true,next_date);        /*停止一个job,里面参数true也可是false，next_date（某一时刻停止）也可是sysdate（立刻停止）。   */

 

存job信息的表user_jobs主要字段说明：

 

列名    数据类型    解释

JOB    NUMBER    任务的唯一标示号

LOG_USER    VARCHAR2(30)    提交任务的用户

PRIV_USER    VARCHAR2(30)    赋予任务权限的用户

SCHEMA_USER    VARCHAR2(30)    对任务作语法分析的用户模式

LAST_DATE    DATE    最后一次成功运行任务的时间

LAST_SEC     VARCHAR2(8)    如HH24:MM:SS格式的last_date日期的小时，分钟和秒

THIS_DATE    DATE     正在运行任务的开始时间，如果没有运行任务则为null

THIS_SEC    VARCHAR2(8)     如HH24:MM:SS格式的this_date日期的小时，分钟和秒

NEXT_DATE    DATE    下一次定时运行任务的时间

NEXT_SEC    VARCHAR2(8)    如HH24:MM:SS格式的next_date日期的小时，分钟和秒

TOTAL_TIME    NUMBER    该任务运行所需要的总时间，单位为秒

BROKEN    VARCHAR2(1)    标志参数，Y标示任务中断，以后不会运行

INTERVAL    VARCHAR2(200)    用于计算下一运行时间的表达式

FAILURES    NUMBER    任务运行连续没有成功的次数

WHAT     VARCHAR2(2000)    执行任务的PL/SQL块

 

===============================================================================重写与重载===================================================================================

 

override（重写）

 

　　 1、方法名、参数、返回值相同。

 

　　 2、子类方法不能缩小父类方法的访问权限。

 

　　 3、子类方法不能抛出比父类方法更多的异常(但子类方法可以不抛出异常)。

 

　　 4、存在于父类和子类之间。

 

　　 5、方法被定义为final不能被重写。

 

　overload（重载）

 

　　1、参数类型、个数、顺序至少有一个不相同。

 

　　2、不能重载只有返回值不同的方法名。

 

　　3、存在于父类和子类、同类中。

 

===============================================================================HTTP PUT方法和POST方法的区别===================================================================================

POST在请求的时候，服务器会每次都创建一个文件，但是在PUT方法的时候只是简单地更新，而不是去重新创建

 

 

 

===============================================================================接口与抽象类===================================================================================

如果是抽象类要实现接口，可以实现部分或者一个都不实现就行，要是具体类搜索就必须实现所有的方法

实现接口或继承抽象类的子类必须实现接口的所有方法或抽象类的所有抽象方法。

接口中的所有方法均为抽象方法，抽象类中包含非抽象方法和抽象方法。

搜索如果一个类实现了接口，那么该子类必须实现父接口的所有方法。如果一个类继承了抽象类，那么该子类必须实现抽象类的所有抽象方法。

 

===============================================================================转发与重定向===================================================================================

转发在服务器端完成的；重定向是在客户端完成的

转发的速度快；重定向速度慢

转发的是同一次请求；重定向是两次不同请求

转发不会执行转发后的代码；重定向会执行重定向之后的代码

转发地址栏没有变化；重定向地址栏有变化

转发必须是在同一台服务器下完成；重定向可以在不同的服务器下完成

 

//转发,转发是在服务器端转发的，客户端是不知道的  

request.getRequestDispatcher("/student_list.jsp").forward(request, response);

//重定向，不会共享request  

response.sendRedirect("/student_list.jsp");   

 

客户首先发送一个请求到服务器端，服务器端发现匹配的servlet，并指定它去执行，当这个servlet执行完之后，

它要调用getRequestDispacther()方法，把请求转发给指定的student_list.jsp,整个流程都是在服务器端完成的，

而且是在同一个请求里面完成的，因此servlet和jsp共享的是同一个request，在servlet里面放的所有东西，

在student_list中都能取出来，因此，student_list能把结果getAttribute()出来，getAttribute()出来后执行完把结果返回给客户端。整个过程是一个请求，一个响应。

 

客户发送一个请求到服务器，服务器匹配servlet，这都和请求转发一样，servlet处理完之后调用了sendRedirect()这个方法，这个方法是response的方法，

所以，当这个servlet处理完之后，看到response.senRedirect()方法，立即向客户端返回这个响应，响应行告诉客户端你必须要再发送一个请求，

去访问student_list.jsp，紧接着客户端受到这个请求后，立刻发出一个新的请求，去请求student_list.jsp,这里两个请求互不干扰，相互独立，

在前面request里面setAttribute()的任何东西，在后面的request里面都获得不了。可见，在sendRedirect()里面是两个请求，两个响应。

 

当用RequestDispatcher请求转发后，地址栏为http://localhost:8080/test/TestServlet

当用sendRedirect重定向后，地址栏为http://localhost:8080/test/student_list.jsp

 

 

ModelAndView mav = new ModelAndView("redirect:/login/index.action");

 

===============================================================================JAVA 消息队列的使用场景===================================================================================

假设你的服务器每分钟的处理量为200个，但客户端再峰值的时候可能一分钟会发1000个消息给你，

这时候你就可以把他做成队列，然后按正常有序的处理，先进后出(LIFO)，先进先出(FIFO）可根据自己的情况进行定夺

 

个人认为消息队列的主要特点是异步处理，

主要目的是减少请求响应时间和解耦。所以主要的使用场景就是将比较耗时而且不需要即时（同步）返回结果的操作作为消息放入消息队列。

同时由于使用了消息队列，只要保证消息格式不变，消息的发送方和接收方并不需要彼此联系，也不需要受对方的影响，即解耦和。

 

使用场景的话，举个例子：

假设用户在你的软件中注册，服务端收到用户的注册请求后，它会做这些操作：

1.校验用户名等信息，如果没问题会在数据库中添加一个用户记录

2.如果是用邮箱注册会给你发送一封注册成功的邮件，手机注册则会发送一条短信

3.分析用户的个人信息，以便将来向他推荐一些志同道合的人，或向那些人推荐他

4.发送给用户一个包含操作指南的系统通知

5.等等……

但是对于用户来说，注册功能实际只需要第一步，

只要服务端将他的账户信息存到数据库中他便可以登录上去做他想做的事情了。

至于其他的事情，非要在这一次请求中全部完成么？!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

值得用户浪费时间等你处理这些对他来说无关紧要的事情么？

所以实际当第一步做完后，服务端就可以把其他的操作放入对应的消息队列中然后马上返回用户结果，

由消息队列异步的进行这些操作。

 

或者还有一种情况，同时有大量用户注册你的软件，再高并发情况下注册请求开始出现一些问题，

例如邮件接口承受不住，或是分析信息时的大量计算使cpu满载，这将会出现虽然用户数据记录很快的添加到数据库中了，

但是却卡在发邮件或分析信息时的情况，导致请求的响应时间大幅增长，甚至出现超时，这就有点不划算了。

面对这种情况一般也是将这些操作放入消息队列（生产者消费者模型），消息队列慢慢的进行处理，同时可以很快的完成注册请求，

不会影响用户使用其他功能。

 

所以在软件的正常功能开发中，并不需要去刻意的寻找消息队列的使用场景，而是当出现性能瓶颈时，去查看业务逻辑是否存在可以异步处理的耗时操作，如果存在的话便可以引入消息队列来解决。

否则盲目的使用消息队列可能会增加维护和开发的成本却无法得到可观的性能提升，那就得不偿失了。

 

===============================================================================小知识============================================================================

HashSet的底层就是HashMap，set的contain相当于map的keySet

ArrayList是Object类型的数组，初始值是10

 

List是有序的,是以数组的存储方式进行存储.也就是说数组什么样它就什么样,,唯一的区别就是,它没有固定大小.

且List的检索效率比较高,不过要频繁的对这个容器里的元素进行更新就不要用它了,用linkedlist比较好.

 

ArrayList类似于数组，是按顺序存储在内存的。

LinkedList类似与链表，是没有顺序的，是通过指针链接了每个元素。

因为LinkedList是无序存储的，所以插入随便一个地方都可以，只要指针指向了就行。

而ArrayList是有序的，插入要遍历到你要插入的位置，所以效率低些。

正因为ArrayList是有序的，所以查询的时候输入索引，就可以很快找到，LinkedList则不然。

 

list有序，可重复  set无序不可重复。

此处有序无序，是指存储的位置是不是有序的

===============================================================================redis===================================================================================

[Http://redis.io](http://redis.io/)

[Http://www.redis.cn](http://www.redis.cn/)

 

linux中查看redis有没有启动： ps -ef|grep redis

​                             lsof -i :6379

​                             启动： redis-server /xx/redis.conf

​                                    redis-cli -p 6379

 

redis挡在mysql前面，替他分担一部分。为什么要挡mysql前面，成千上万个请求操作数据库，数据库会崩，数据库是要设置并发量的，mysql默认是100，第101个请求过来了，

会先等待，100个人中哪个先处理完了，再来处理这个101个请求。

 

redis替代memCached

！！！！！！！！！！！！！！！！！！！！！！！！redis：将高频热点的数据放到redis中！！！！！！！！！！！！！！！！！！！！

传统的关系型数据库：范式 + 1:1/1:N/N:N + 主外键

NoSQL:易扩展（传统关系型数据库加其他列）且支持多种数据类型，BSON：类json的一种二进制形式的存储格式

NoSQL的数据模型：聚合模型：KV键值对（redis）、BSON、列族（按列存储数据，纵向拓展）、图形

分布式系统忌讳多表关联查询

 

MongoDB：基于分布式文件存储的数据库

HBase：列存储数据库

 

传统ACID:

A:原子性：要么全部完成要么都不做

C:一致性: 数据库要处于一致的状态，事务的运行不会改变原本的一致性约束

I:独立性: 并发的事务之间不会相互影响，一个事务访问的数据正在被另一个事务修改，只要另一个事务未提交，就没事

D:持久性: 一旦事务提交后，它所做的修改会永久的保存在数据库中

 

分布式数据库：CAP原理 + BASE：

C:强一致性:Consistency （数据精确：点赞数是140还是141）

A:可用性：Available （网站崩溃了）

P:分区容错性:Partition tolerance  （分布式）

CAP只能3选2，因此根据CAP原理将NoSQL数据库分成了满足CA原则，满足CP原则，满足AP原则：

CA:单点集群，满足一致性、可用性的系统，在可拓展性上不太强大  ====》 传统的关系型数据库 RDBMS

CP：满足一致性、分区容忍性的系统，通常性能不是特别高。 ===》redis、mongoDB、Hbase    NoSQL

AP：满足可用性、分区容忍性的系统，通常一致性不是特别高。淘宝京东等大型网站就是用的这个

 

NoSQL：分区容错性必须要实现。

 

Base理论：解决关系数据库强一致性引发的问题而引起的可用性降低而提出的解决方案。

基本可用:

软状态：

最终一致：双11过了之后 数据一定是精确的

 

分布式的思想：通过让系统放松某一时刻数据一致性的要求来换取系统整体伸缩性和性能上的改观。大型系统往往由于地域分布和极高性能的要求，

不可能采用分布式事务来完成这些指标，想要获得这些指标，用BASE这个方案

 

分布式+集群：

负载均衡:多台TOMCAT，请求平均

分布式：不同的多台服务器上面部署不同的服务模块，它们之间通过Rpc/Rmi通信和调用，对外提供服务和组内协作。

集群：  不同的多台服务器上面部署相同的服务模块，通过分布式调度，对外提供服务和访问。一台sql搞不定装4台

 

 

REDIS: KV + cache + persist

高性能的key/value分布式内存数据库，是Nosql数据库之一，redis是内存

3大特点：

Redis支持数据的持久化，可将内存中的数据保存在磁盘中，重启的时候可以再次加载使用，即内存存储和持久化，支持异步将内存中的数据写到硬盘上，断电重启后数据还在。

Redis不仅仅支持key/value类型的数据，同时还支持list、set、zset、hash等数据结构的存储。

Redis支持数据的备份，即master-slave模式的数据备份。

 

redis 5+1 ： 5大数据类型 + key

redis默认16个数据库，从0-15

select 0、select 1  来切换

select命令来切换数据库

dbsize查看当前数据库的key的数量

keys * 查看所有的key

keys k? 查出k开头的key

flushdb 清理当前数据库的内容

flushall

exists xx : 是否存在xx这个key

move k3 2 ：将k3这个key移到2号库

ttl key ：查看还有多少秒过期，-1永不过期 -2已过期 ttl：time to live，已过期的就要移出内存。被清除了

setex k1 10 v1 :活10秒

setnx ： set if not exist； set k1 v1 ； setnx k1 v12； v12不会设置成功。  set if not exist

type key ： 查看key是什么类型

del key ：删除key

set k1 v1 , set k1 v2 : 覆盖

type key ： 查看key是什么类型

lpush mylist 1 2 3 4 5 ; lrange mylist 0 -1; : 5 4 3 2 1    type mylist : list

set k1 v1; append k1 v2; get k1 ==> k1v2; strlen k1 ==> 4

incr/decr/incrby/decrby : 数字才能加减  incr k1; incrby k1 3;

set k1 ty12345; getrange k1 0 -1 == > ty12345;  getrange k1 0 3 ==> ty12

setrange设置指定区间范围内的值 ： setrange key值 具体值：

set k1 abcd1234; setrange k1 1 xxx == > axxx1234;

setrange，getrange ： 范围内设值，取值

mset、mget、msetnx ： mset k1 v1 k2 v2 k3 v3; mget k1 k2 k3 ==>  v1 v2 v3    m:more

msetnx k3 v3 k4 v4 ==》 k3已存在 k4不存在的情况下 结果：0  失效

 

STRING:

append:在某一个key上追加一个值 append message hello；

​                               append message world；

​        结果：  get message：helloworld                           

 

 

LIST:  字符串链表

LPUSH RPUSH LRANGE；  LPUSH 可以一次性塞好几个值， LPUSH myList 1 2 3 4 5， list结果： 左边是第一个数

lpop rpop

lindex mylist 3 : mylist索引是3的元素

llen mylist；

lset keyVal index val；替换某一个index上的值

linsert keyVal before/after val1 val2; 插

总结： redis 的list 是一个字符串链表，左右都可以插入。链表的操作无论是头还是尾，效率都很高，但如果对中间元素操作，则效率低下

 

SET：和list差不多，就是不能重复

sadd，smembers，sismember；      sadd 可以一次性塞好几个值， sadd mySet 1 2 3 4 5， set结果：无序，不重复

smembers set01 ==》打印set01  

sismember set01 x ==》判断x是不是在set01中，结果0  1

scard：获取集合里元素的个数。  scard set01

srem：删除集合里某个元素   srem set01 3； 此处3是val而不是index

spop： set是无序的，spop也即随机出栈

差集：sdiff

交集：sinter   ====  inner join

并集：sunion

 

Hash：重要  类似map<String,Object>

KV模式不变但是V是一个键值对

hset：hset user id 11；  hget user id ===》11

hmset user id 11 name lisi age 26; hmge user id name age; ==> 11 lisi 26

或者：hgetall user;===> id 11 name lisi age 26

hdel user name;==>删除一个属性

hlen user；===》user中有几个属性

hexists key1 key2==》key1里是否有key2

hexists user id ==》 1

hkeys user ==》 id name age

hvals user ==》 11 lisi 26

hincrby(整数)/hincrbyfloat(小数)  => 属性的值增长

hsetnx user age 26; ==> 0   hsetnx user email [11@qq.com](mailto:11@qq.com); ==> 1

 

Zset:2个一个整体

在set基础上加上一个score值，之前set是 k1 v1 v2 v3,现在 zset 是 k1 score1 v1 score2 v2 score3 v3

zadd zet01 60 v1 70 v2 80 v3 90 v4 100 v5;   

zrange zet01 0 -1 ==> v1 v2 v3 v4 v5

zrange zet01 0 -1 withscores==> v1 60 v2 70 v3 80 v4 90 v5 100

zrangebyscore zet01 60 90 ==> v1 v2 v3 v4

( : 不包含  zrangebyscore zet01 60 (90 ==> v1 v2 v3

​            zrangebyscore zet01 (60 (90 ==> v2 v3

limit：开始下标数 多少步  ==》 像分页

​            zrangebyscore zet01 60 90 limit 2 2 ==》v3 v4

zrem zet01 v5 ==》把v5删了

zcard 统计个数： zcard zet01 ==> v5删了后，结果4    

zcount key score区间 ： zcount zet01 60 80 ==》结果3             

zrank key val值：获取下标值    ：zrank zet01 v4 ==> 3    (下标是0开始)

zscore key1 key2：获得分数 ： zscore zet01 v4 ==》90

zrevrank key val值：逆序获取下标值    zrevrank zet01 v4 ==> 0    (下标是0到3)

zrevrange zet01 0 -1 ==》 v4 v3 v2 v1

zrevrangebyscore zet01 90 60 ==》 v4 v3 v2 v1

​            

redis索引从0开始，默认端口6379，merz歌手

 

REDIS 5+1 ： 五大数据类型 + key

REDIS五大数据类型：

String：二进制安全的，redis的String可以包含任何数据，比如jpg图片或者序列化的对象，一个key一个value

List ：底层是链表，类似LinkedList，链表是双向的，前后都可以塞

Set：String类型的无序集合，不重复

Hash ：类似map<String,Object> 是一个键值对集合,适合存储对象

Zset（Sorted set）：String类型的有序集合，不重复，与set不同的是每个元素关联一个double类型的分数，zset的成员是唯一的，但是分数是可以重复的

[Http://redisdoc.com](http://redisdoc.com/)  redis命令参考大全

 

REDIS配置文件： 重要

redis.conf

1.配了端口 6379

2.config get dir ： redis在哪个下面启动，配置文件就生成在哪个目录下

启动： redis-server /xx/redis.conf

​       redis-cli -p 6379

3.maxmemory-policy noeviction 默认是永不过期的策略，实际项目是要改

缓存过期清洁策略：

volatile-lru ： 使用LRU算法移除key，只对设置了过期时间的键

allkeys-lru  ：使用LRU算法移除key

volatile-random ： 在过期集合中移除随机的key

volatile-ttl ： 移除最近要过期的key

noeviction ： 永不过期

 

 

redis可以做缓存服务器、消息中间件，是一个分布式的内存数据库

 

redis持久化：rdb aof

rdb： Redis DataBase

​      是什么： 在指定的时间内将内存中的数据集快照写入磁盘，也即Snapshot快照，

​      它恢复时将快照文件直接读到内存中，一断电内存中会消失，将快照文件直接读到内存中

​      redis会单独创建（fork）一个子进程来进行持久化，会先将数据写入到一个临时文件中，

​      待持久化结束了，再用这个临时文件替换上次持久化好的文件(dump.rdb)。

​      ！！！！整个过程中，主进程不进行任何IO操作，主进程唯一做的就是fork一个子进程！！！！，保证了性能

​      如果需要进行大规模数据的恢复，且对于数据恢复的完整性不是非常敏感，那ROB比AOF更加高效

​      RDB缺点：最后一次持久化后的数据可能丢失

​      相当于备份时保证源文件是静态的      

​      

​      fork作用：复制一个与当前进程一样的进程，新进程的所有数据都和原进程一样，但是是一个全新的进程

​      作为原进程的子进程。

​      如果redis进程很大，此处是个隐患

​      

​      将内存中的数据集快照写入磁盘上，写在磁盘上的dump.rdb文件中

​      

​      配置位置：redis.conf 中的snapshotting中

​      save <seconds> <changes>

​      save "" 是禁用的意思

​      默认配置 //出厂默认配置： 1分钟该10000次，5分钟改10次，15分钟改一次 //面试要问

​      save 900 1

​      save 300 10

​      save 60 10000

​      只要900s内改过一次，（不是get），300s内改过10次，就会自动触发rdb文件生成

​      也可以手动保存：比如set一条数据数据了，直接save命令，会立即备份生成dump.rdb文件，save时redis阻塞

​      bgsave：异步保存

​      flushall命令也会生成dump.rdb文件，但是里面的内容是空的。

​      

​      也即：主进程在操作redis缓存的时候，只要触发了上述事件，会有一个子进程来备份数据,生成dump.rdb文件，此文件用来恢复时将数据加载回内存。

​      此处会有存储过程用来周期的将dump.rdb文件再次备份到其他服务器上，防止保存dump.rdb的那个机器坏了。即：备份的机器和要恢复的机器不是同一台

​      如何恢复： 先shutdown，将备份的dump.rdb文件移到redis安装目录，并启动服务

​      

​      劣势：fork的时候，内存中的数据也会被复制一份，2倍的膨胀性

​            最后一次的数据可能会意外丢失

​      优势：与aof相比，在恢复大的数据集时 rdb更快

​      

aof： Append Only File

​      在redis_conf配置文件中： appendOnly 默认是 No,要把他改成 yes

​      Appendfsync： Always：同步持久化，每次发生数据变更会立即记录到磁盘，性能较差但数据完整性较好

​                    EverySec：出厂默认设置，异步操作，每秒记录，如果一秒内挂机了，会有数据丢失

​      aof文件有序的保存了对数据库执行的所有写入操作

​      以日志的形式来记录每个写操作，只能追加文件，不能改写文件，redis启动之初会读取该文件重新构建数据

​      AOF保存的是appendonly.aof文件,aof:每秒中你写什么操作,我备份什么.每一秒都在写,如果在写的过程中断电了,写了一半

​      导致appendOnly.aof文件损坏，此时可以用 redis-check-aof --fix appendonly.aof 命令来修复此文件

​      

​      dump.rdb 和 appendOnly.aof是可以共存的，先加载的是 appendOnly.aof

​      

​      rewrite：

​      aof采用文件追加，在高并发的情况下，redis中 用户 incr k1执行了100W次，aof中也会依次执行100w 次。

​      为此，新增了重写机制，当aof文件大小超过了所设定的阈值，会启动内容压缩，只保留最小的指令集，命令是

​      bgrewriteaof：

​      原理：aof持续增长，会fork出一个新进程来将文件重写，并没有读取旧的aof文件，而是将整个数据库的内容用命令的方式重写

​      一个新的aof，即直接参照数据库，而非aof文件，数据库中k1式100w，则直接 incr k1 100w，而非 incr k1 执行100w次。

​      触发机制：redis会记录上次重写时的aof文件大小，默认是 当aof文件大小是上次rewrite后大小的一倍且文件大于64M时触发

​      这个写在配置文件中： auto-aof-rewrite-min-size 64mb   auto-aof-rewrite-percentage 100

​      

​      aof优势：每秒同步、每修改同步、不同步 灵活的策略，数据完整性高，每秒同步，最恶劣只丢失一秒内的数据。

​      劣势：相同数据集的数据而言，aof文件远大于rdb文件，恢复速度慢于rdb，因为其频繁的IO和重写，这个过程阻塞不可避免

​      

​      综上：

​      如果你只是希望你的数据在服务器运行的时候存在，只作为缓存，则可以不使用任何持久化方式。redis：kv+cache+persist

​      persist持久化的目的 就是备份数据 使得系统重启后 缓存中的数据还在

​      速度要快，但是数据敏感性完整性要求低的话，则采用rdb形式，他是在指定的时间间隔内，对数据进行快照存贮

​      

​      官网建议：同时开启2种持久化方式，默认是先加载aof的文件，这是因为通常aof文件的数据集要比rdb文件数据集完整性高。

​      rdb文件的数据不实时

​      那为什么不只用aof呢 应为aof在不停的变化，不适合备份，留一个万一的手段

​      

​      方案：使用Master-Slave Replication ,可以省掉一大笔IO，代价是如果Master-Slave同时倒掉，会丢失10多分钟的数据，启动脚本也要比较

​      Master-Slave中的rdb数据，选用较新的那个rdb，新浪微博采用了这个方案。

 

redis复制：master/slave 主从复制，读写分离：主机数据更新后根据配置和策略，自动同步到备机的master/slaver机制，master以写为主，slaver以读为主，slaver不能写。

   复制的原理：

​      slaver连接到master后会发送一个sync命令，（同步的命令），首次是全量复制：master将整个数据库文件传给slave，完成一次完全同步.

​      同步完成之后,master又陆续有新的修改命令,此时再增量复制,只把新增加的修改命令传给slaver,完成同步.slaver只要一重新连接到master,

​      一次全量复制自动执行.

   形式一： 一主多从

​      A------B

​         |___C      

​      主从的意思是在一台机器上，主redis的端口是6379，另开两个redis只要确保他们的端口不同即可，也即：另外复制2份redis.conf配置文件，在里面把

​      redis端口改了，启动好几个redis形成集群

​      1.配从库不配主库，从库配置： slaveof 主机IP 主机端口

​            info replication：查看当前端口的redis是什么地位，什么角色，默认不配的，各个都是主机

​            从机上：slaveof 主机ip 主机redis端口，从机只要一slave，就会把主机上缓存中所有的数据都备份下来。

​      2.读写分离：只有主机可以set，从机上只能读，不能set

​      3.主机死了，从机里数据还在，从机info replication ：依旧还是slave； 5min后主机恢复了，从机原地待命，不会上位，主从关系不变。（领导出差）

​      4.现在有一台备机死了，其他设备的主从关系不变； 5min后从机恢复了，次从机变成了默认的一台主机，需要再配置slaveof 主机IP 主机端口，才行

​      只要从机与主机断开了，就要重新连一次，手动配置主从关系，除非写进配置文件

   形式二： 薪火相传

​      如果多台从机全挂在一台主机上，主机的负担太重,例如： A上面挂了BCDEFGHIGKLM ,可以改成这种树状结构：

​      A----B----E

​      |    |____F

​      |    |____G

​      |

​      |____C----HIG    

​      |____D----KLM    

​      

​      上一个slaver可以是下一个slaver的master，中途变更转向，会清除之前的数据，重新建立拷贝最新的。slaveof 新主机IP 新主机端口

​      上图中B这个从机的 info replication： 仍然是个slaver，但是他可以连接其他slaver

​      毛病：备份的延时

   形式三： 反客为主

​      主机挂了，手动的让某一个从机成为主机：slaveof no one相当于解除主从关系,自己变成一个没有slave的master，

​      其他的从机此时仍然原地待命，想要跟新老板，也需要手动配下slaveof 新主机IP 新主机端口

​      其他从机跟了新老板后，原先挂了的主机回来后：从新变成一个默认的下面没有slaver的主机。

​      问题:需要手动配置,那么凌晨主机挂了呢.

   形式四： 哨兵模式sentinel（最优，可以代替前3种模式:反客为主的自动版）  

​      主机挂了,在剩下的从机器中,采用投票的方式,选举出主机.

​      步骤:1.在redis.conf的目录下,新建一个sentinel.conf文件:  touch sentinel.conf

​           2.vim sentinel.conf;  2.1 sentinel monitor 被监控主机名字(随便起一个名字) 被监控主机IP 被监控主机端口 1

​             这个地方的1指的是主机挂掉后，剩下从机投票谁多余1票，谁就是主机。

​           3.启动哨兵： 在bin目录下有 redis-sentinel命令； 所以在该目录下：redis-sentinel /xx/xx/sentinel.conf

​           4.剩下的从机投票确认好主从关系后，如果此时原来挂掉的主机回来了。哨兵会让他做slaver。   

redis 事务：

​      常用命令：discard  exec  multi unwatch watch

​      multi     : 开启事务

​      set k1 v1 : 返回queued  直接入队，并没有执行

​      get k1    : 返回queued

​      set k2 v2 : 返回queued

​      exec      ：执行事务

​      结果：

​      ok

​      "v1"

​      ok

​      

​      multi     : 开启事务

​      set k1 v1 : 返回queued  直接入队，并没有执行

​      get k1    : 返回queued

​      discard   ：结束事务，上面的2条命令相当于没有执行

​      

​      连坐：     在事务的过程中，有一条命令直接语法报错了，例如：getset k1，直接报错：error 则该事务中其他的命令也会失效

​      冤头债主 ：在事务的过程中，有一条命令语法没错了，胆识逻辑错了，例如：set k1 v1 ; incr k1 ，结果：queued 则该事务中其他的命令不会失效

​      类似： java 中 int a = 10/0；会放行，运行的时候才知道

​      redis对事务的支持是部分支持，不像oracle一样绝对强一致性：冤头债主，对的放行，错的挂了

​      

​      watch监控： watch使用场景：需要加锁的变量，也即在要修改的时候，watch unwatch，watch是乐观锁机制

​            乐观锁，悲观锁，cas（check and set）

​            拓展：mysql的行锁与表锁   表锁：并发性极差，但一致性极好，类似于悲观锁

​            乐观锁：在每一条记录最后加一个标志：version版本号，例如2个人同时取得一条记录，然后修改，同时取得时version=1

​            每次修改version+1，a先提交完，version=2，b再提交时version与获取时的不一样，则会报错，要求重新查再改。

​            工作中用到的：一般是要用乐观锁，为了满足并发性

​            悲观锁:读数据时总有人在改，所以每次拿数据时都会加上锁，传统型关系数据库 行锁与表锁 读锁写锁 都是用之前先上锁。

​            乐观锁：读数据时没有人在改，所以不会上锁，但是在更新的时候会判断一下别人在此期间有没有更新过这个数据，使用版本号这个机制

​            乐观锁策略：提交版本必须大于记录当前版本才能执行更新

​            乐观锁缺点：只有在提交操作的时候检查是否违反数据完整性。只能防止脏读后数据的提交，不能解决脏读。

​            悲观锁：比较适合写入操作比较频繁的场景，如果出现大量的读取操作，每次读取的时候都会进行加锁，这样会增加大量的锁的开销，降低了系统的吞吐量。

​            乐观锁：比较适合读取操作比较频繁的场景，如果出现大量的写入操作，数据发生冲突的可能性就会增大，为了保证数据的一致性，应用层需要不断的重新获取数据，这样会增加大量的查询操作，降低了系统的吞吐量。

​            总结：两种所各有优缺点，读取频繁使用乐观锁，写入频繁使用悲观锁。在实际生产环境里边,如果并发量不大且不允许脏读，

​            可以使用悲观锁解决并发问题；但如果系统的并发非常大的话,悲观锁定会带来非常大的性能问题,所以我们就要选择乐观锁定的方法.

​            所以悲观锁和乐观锁最大的区别是是否一直锁定资源搜索，悲观锁在事物的全流程锁定数据，乐观锁不锁定数据，

​            悲观锁和乐观锁的重点就是是否在读取记录的时候直接上锁。悲观锁的缺点很明显，需要一个持续的数据库连接，这在web应用中已经不适合了。

​            

​            乐观锁的例子：

​            a. 假设当当网上用户下单买了本书，这时数据库中有条订单号为001的订单，其中有个status字段是’有效’,表示该订单是有效的；

​            b. 后台管理人员查询到这条001的订单，并且看到状态是有效的

​            c. 用户发现下单的时候下错了，于是撤销订单，假设运行这样一条SQL: update order_table set status = ‘取消’ where order_id = 001;

​            d. 后台管理人员由于在b这步看到状态有效的，这时，虽然用户在c这步已经撤销了订单，可是管理人员并未刷新界面，（仅仅是因为用户界面没有刷新，事实上也不可能做自动刷新，

​            这样相当于数据库一发生改变立刻要刷新了，这需要监听数据库了）

​            看到的订单状态还是有效的，于是点击”发货”按钮，将该订单发到物流部门，同时运行类似如下SQL，

​            将订单状态改成已发货:update order_table set status = ‘已发货’ where order_id = 001

​            

​            乐观锁实现：在sql里实现 ：在创建表时，每一条数据库记录后加一个字段 version，查和更新是分离的

​            update account_wallet set user_amount = #{userAmount,jdbcType=DECIMAL}, version = version + 1 where id =#{id,jdbcType=INTEGER} and version = #{version,jdbcType=INTEGER}

 

​            set balance 100； set debt 0；

​            watch balance；

​            multi

​            decrby balance 20;

​            incrby debt 20;

​            exec;    结果：80 20

​            

​            现在如果：在watch balance之后 multi之前，另一个线程 set balance 200；

​            watch balance；

​            multi

​            decrby balance 20;

​            incrby debt 20;

​            exec;    结果：nil，事务提交失败

​            get balance ： 200 像乐观锁，要重新查一遍再更新

​            

​            watch key[，key1，key2]

​            一旦执行了exec，默认会unwatch

​            unwatch：取消对所有key的监视

​            

​            小结：watch是乐观锁机制，如果在事务提交之前，key的值被其他用户给修改了，则事务不会执行，返回Nullmulti-bulk事务失败，需要重新读key

​            的值，再执行更新一遍。

​            redis事务3阶段： 开启-入队-执行

​            特性：不保证原子性，部分支持事务

 

​            

redis_jedis

​      1.在java中连接redis：

​        以前是eclipse连接mysql数据库，现在是连接nosql缓存数据库

​        Jedis jedis = new Jedis(主机IP,主机端口);

​        jedis.ping();  PONE

​      2.api   参考jedis api

​        jedis.select(2)

​        //key

​        Set<String> set = jedis.keys(String xx)；  .keys("*")

​        jedis.exists(String key);

​        jedis.ttl(String key);

​        

​        //String

​        jedis.append(String key,String value);  //key已经存在了，value追加到其val之后

​        jedis.set(String key,String value)  ==>写到redis中

​        jedis.get(String key)；   

​        jedis.mset("k1","v1","k2","v2","k3","v3");

​        jedis.mget("k1","k2","k3");

​        

​        //list

​        jedis.lpush("myList","k1","k2","k3");             lpush(String key, String... strings)

​        List<String> ll = jedis.lrange("myList",0,-1);    lrange(String key, long start, long end)

​        

​        //set

​        sadd(String key, String... members)

​        Set<String> smembers(String key)

​        srem(String key, String... members)

​        

​        //hash

​        hset(String key, String field, String value)

​        String hget(String key, String field)

​        hmset(String key, Map<String,String> hash)

​        List<String> hmget(String key, String... fields)

​        

​        //zset

​        zadd(String key, double score, String member)

​        zadd(String key, Map<Double,String> scoreMembers)

​        Set<String>    zrange(String key, long start, long end)

​      3.事务 cas ： check and setting

​        Transaction  t = jedis.multi();   //开启

​        t.set(String key, String val) ;   //入队

​        t.exec();                         //执行

​        t.discard();                      //回滚

​        

​        锁:  乐观锁机制

​        watch: watch命令就是标记一个key,如果在事务提交之前,这个key被其他人修改过,则事务提交exec失败.程序捕获这个错误

​               程序再重新尝试一次.

​        

​        int  balance;         //银行余额

​        int  debt;            //信用卡        

​        int  amtoSubtract;    //实刷额度

​        jedis.watch(balance);

​        // 模拟其他线程修改了balance

​        jedis.set("balance",5)

​        //

​        balance = Integer.parseInt(jedis.get("balance"));

​        if(balance < amtoSubtract){

​             sysout(balance被修改了);

​             jedis.unwatch();

​             return false;

​        }

​        Transaction  t = jedis.multi();

​        t.decrBy("balance",amtoSubtract);

​        t.incrBy("debt",amtoSubtract);

​        t.exec();

​        

​        balance = Integer.parseInt(jedis.get("balance"));

​        debt = Integer.parseInt(jedis.get("debt"));

​        return true;

​     4.主从复制,读写分离

​        Jedis jedis_M = new Jedis(主机IP,主机端口1);

​        Jedis jedis_S = new Jedis(主机IP,主机端口2);

​        jedis_S.slaveof(主机IP,主机端口1);

​        jedis_M.set(x,xx);

​        jedis_S.get(x);

​     5.数据库连接池，线程池，多个Jedis实例

​       多个new会消耗系统内存。

​       当一个Web服务器接受到大量短小线程的请求时，使用线程池技术是非常合适的，

​       它可以大大减少线程的创建和销毁次数，提高服务器的工作效率。

​       但如果线程要求的运行时间比较长，此时线程的运行时间比创建时间要长得多，单靠减少创建时间对系统效率的提高不明显，

​       此时就不适合应用线程池技术，需要借助其它的技术来提高服务器的服务效率。

​    

​    public class JedisPoolUtil{

​    private JedisPoolUtil(){}

​    private static volatile JedisPool jedisPool = null;

​    public static JedisPool getInstance(){

​        if(null == jedisPool){    

​            synchronized(JedisPool.class){

​               if(null == jedisPool){

​                   JedisPoolConfig poolConfig = new JedisPoolConfig();

​                   poolConfig.setMaxActive(1000);

​                   poolConfig.setMaxIdle(32);

​                   poolConfig.setMaxWait(100*1000);

​                   poolConfig.setTestOnBorrow(true);

​                   jedisPool = new JedisPool(poolConfig,IP,端口);

​               }

​            }

​         }

​         return jedisPool;

​    }

​    

​    public static void release(JedisPool jedisPool,Jedis jedis){

​        if(null != jedis){

​            jedisPool.returnResourceObject(jedis);

​        }

​    }

​    }

​    

​    

redis内存优化手段与参数：

首先最重要的一点是不要开启Redis的VM选项，即虚拟内存功能，

这个本来是作为Redis存储超出物理内存数据的一种数据在内存与磁盘换入换出的一个持久化策略，

但是其内存管理成本也非常的高，并且我们后续会分析此种持久化策略并不成熟，所以要关闭VM功能，请检查你的redis.conf文件中 vm-enabled 为 no。

其次最好设置下redis.conf中的maxmemory选项，该选项是告诉Redis当使用了多少物理内存后就开始拒绝后续的写入请求，

该参数能很好的保护好你的Redis不会因为使用了过多的物理内存而导致swap,最终严重影响性能甚至崩溃。

另外Redis为不同数据类型分别提供了一组参数来控制内存使用，我们在前面详细分析过Redis Hash是value内部为一个HashMap，如果该Map的成员数比较少，则会采用类似一维线性的紧凑格式来存储该Map, 即省去了大量指针的内存开销，这个参数控制对应在redis.conf配置文件中下面2项：

hash-max-zipmap-entries 64

hash-max-zipmap-value 512

hash-max-zipmap-entries

含义是当value这个Map内部不超过多少个成员时会采用线性紧凑格式存储，默认是64,即value内部有64个以下的成员就是使用线性紧凑存储，超过该值自动转成真正的HashMap。

hash-max-zipmap-value 含义是当 value这个Map内部的每个成员值长度不超过多少字节就会采用线性紧凑存储来节省空间。

以上2个条件任意一个条件超过设置值都会转换成真正的HashMap，也就不会再节省内存了，那么这个值是不是设置的越大越好呢，答案当然是否定的，HashMap的优势就是查找和操作的时间复杂度都是O(1)的，而放弃Hash采用一维存储则是O(n)的时间复杂度，如果

成员数量很少，则影响不大，否则会严重影响性能，所以要权衡好这个值的设置，总体上还是最根本的时间成本和空间成本上的权衡。

同样类似的参数还有：

list-max-ziplist-entries 512

说明：list数据类型多少节点以下会采用去指针的紧凑存储格式。

list-max-ziplist-value 64

说明：list数据类型节点值大小小于多少字节会采用紧凑存储格式。

set-max-intset-entries 512

说明：set数据类型内部数据如果全部是数值型，且包含多少节点以下会采用紧凑格式存储。

 

 

​    

​    

！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！记住这个场景    

更新缓存：采用的策略：  先更新数据库，再删除缓存

删除缓存后，再从缓存中读数据时，如果没有读到，就从数据库中读取数据，成功后，放入缓存。

这种情况下存在并发的问题，

缓存中没值，A做查询，B做更新， A查询数据库，得到一个旧值，B更新数据库写入新值，B删除缓存，A将查到的旧值写入缓存。

怎么解决此并发：

1.给缓存设置过期时间

3.异步延时删除策略，保证读请求完成后，再进行删除操作。在更新数据库后，过个1秒后，异步的删除缓存。增大吞吐量

public void write(String key,Object obj){

​     db.updateData(obj);

​     Thread.sleep(1000);

​     redis.delKey(key);

}

此方案好存在一个漏端： 删除缓存失败会产生不一致问题，解决方案：（仅适用于删除缓存失败的时候）

一：  1更新数据库，2将删除失败的key发送至消息队列，3自己消费消息，获得要删除的key 4继续重试删除操作，直到成功   

二：  启动一个订阅程序去订阅数据库的binlog，订阅程序获取需要操作的数据key。在应用程序中，另起一段程序，获取这个订阅程序传来的消息，再进行删除缓存操作。

 

 

 

给缓存设置过期时间，是保证最终一致性的解决方案

1.设置 key的生存时间，过期自动删除

　　exprire key  seconds    设置过期时间 秒数

　　ttl key   查询剩余时间

如果 设置了过期时间。对key进行 set 操作，会清除掉 key的过期时间

 

实际例子1： 可以实现  限制频率操作：   

　　如，限制 1分钟的 ip只能访问5次   1.设置 ip为key ，的生存时间为1分钟。2.每次访问，将 访问的时间存入一个 列表中        

实际例子2： 缓存

　　经常访问的数据设置过期时间，访问如不存在就去 查数据库，并存入redis，如存在，就直接从redis取

 

 

小结：  redis持久化与缓存放到数据库里是2个概念。redis持久化：当 Redis 重启时，缓存中的数据还在。

​        如果redis只是作为缓存，缓存中的数据不在数据库中，则其更新操作用watch机制，即数据直接放入缓存，没有通过数据库

​        如果redis的缓存数据与数据库中数据是同步的，则缓存要设置过期时间，则缓存的更新就要注意了，先更新数据库，再异步延时删除缓存，删除缓存失败的情况下，用消息队列的方式重试机制。

 

使用redis作为缓存，redis本身就能持久化存储数据，数据还需要存入数据库中吗？    redis中存的数据，数据库中是否还要存的问题

结果：redis中的数据可以放在数据库中，也可以不放在数据库中，视情况而定。一般而言，缓存中的数据都是从数据库中读到的，读取缓存的步骤就是，先在缓存中有没有数据，

如果没有的话，就从数据库中加载数据，再放入缓存。

3。redis中缓存一些请求量比较大的数据（这些缓存数据，mysql中需不需要有？？？？？），没必要所有数据都缓存到redis中。

4。之所以从缓存中拿数据会快，是因为缓存的数据存在于内存中，不像mysql的数据是存在磁盘上的，

即不用经过从磁盘加载到内存这个过程（这个过程是非常耗时和低效的），直接从内存获取数据。②数据库存在低速设备上，每次访问数据库，都要经过io，

即从磁盘调入内存的过程。这个才是使用redis等缓存机制的原因。

5。当redis缓存崩溃的时候，那么不是海量的请求都去访问数据库了？数据库能抗住吗？

​       以tomcat、Oracle为例，解释是它们是怎么处理大量并发请求的？

​       tomcat和Oracle的处理请求机制一样。

​       以Oracle为例，如果Oracle设置并发数（即最大连接数，mysql默认是100）是100。

​       场景1：当有99个请求同时过来，怎么办？

​          答：我有100个人，分配99个人，一人去响应一个请求，这样大家并发完成。

​       场景2：当有101个请求同时过来，怎么办？

​          答：我有100个人，分配100个人，一人响应一个请求。但是还剩1个请求没有人响应怎么办？答案是，这个请求等着，等哪个人处理完了，就叫你过去。

\6. 1。前提：mysql中存基本数据，redis中缓存访问量超级大的数据。

   \2. 全把数据放入redis风险不就更大了吗？因为我mysql虽然慢，但是最起码没有丢失，但是你redis是放入内存的，所有数据都丢失了？

redis有灾备机制，因为redis会将其中的数据实时地存入磁盘，这样就不怕丢了。那这不是回到我的思路上了吗？

你存磁盘其实跟存数据库不是一个道理吗？方正都是存磁盘？你怎么能将99G或者更大的数据快速的从磁盘加载到redis即内存中呢？不可能的。

如果redis即内存崩溃了，然后重启redis之后，怎么快速的响应千万甚至过亿的请求。

我的方式：redis坏了，从数据库读取。你的方式：redis坏了，从磁盘慢慢地恢复到redis，然后从redis读取。 这2中方式都不对  ===》 redis集群，主备机

 

正是因为 redis可以持久化，所以redis也可以当数据库用来，redis叫 内存数据库，（mysql叫 磁盘数据库，我自己的理解）

mysql偏向于存数据，redis偏向于快速取数据，但redis查询复杂的表关系时不如mysql，所以可以把热门的数据放redis，mysql存基本数据

redis的持久化，会可能丢失数据，因为redis的持久化，不是实时的，是数据先在内存，再定时的保存到硬盘来达到持久化，当然，这个定时的时间相隔，是可以配置的。

这个配置的时间，如果太短，那么使用redis的效率就低，如果长了，那么可能丢失的数据就会多，所以，要根据自己的业务来取得一个均衡。

从两者的擅长角度来看，数据库擅长的是存储和检索

redis相当于内存数据库，擅长的地方是读    

===============================================================================MongoDB==========================================================

[www.mongodb.org](http://www.mongodb.org/)

1.我们写的java程序是在内存中运行的==》一旦断电，或程序重启，内存中的变量全没了。因此，数据库相当于磁盘，持久化了

关系型数据库： rdbms，非关系型数据库：NoSql，NoSql包含了：文档数据库mongodb；高性能的key/value分布式内存数据库：redis

简单理解：MongoDB存放的是增强版的json（Bson）

 

2.Mongodb的3个概念： 数据库（数据库里放集合），集合（文档的集合），文档（Mongodb中的最小单位）

3.Mongodb语法：

​           use 数据库名

​            \- 进入到指定的数据库中

​            use xx ，会自动连接到xx数据库，第一次向xx中创建文档时，会自动创建xx数据库，use进入到数据库中，db这个值默认就指向它，use只是

​            进入这个数据库，此时数据库还没有创建，同理集合也一样。

​        show collections

​            \- 显示数据库中所有的集合

​        显示创建collection：

​            \- db.createCollection(‘collectionName’)              

​        统计Collection中文档数量：

​            \- db.collectionName.count();

​    

​        \- 向数据库中插入文档

​            \- db.collection.insert()   insert的对象并不是json，是个js里的object，并且如果文档没有指定"_id"属性，

​                                       Mongodb会自动添加一个属性：_id，作为文档的唯一标识，_id可以自己指定，指定了数据库就不会添加了

​                \- insert()可以向集合中插入一个或多个文档

​                db.stus.insert({name:"孙悟空",age:18,gender:"男"})

​                db.stus.insert([{name:"孙悟空",age:18,gender:"男"},{name:"孙悟空2",age:181,gender:"男"}])

​            \- db.collection.insertOne()

​                \- 向集合中插入一个文档

​            \- db.collection.insertMany()

​                \- 向集合中插入多个文档

​                

​        \- 查询数据库中的文档

​            \- db.collection.find()   无条件即查所有文档，.find()可以接受一个对象作为条件参数，不是json，object对象

​                \- 可以根据指定条件从集合中查询所有符合条件的文档

​                \- 返回的是一个数组

​                db.stus.find({_id："Hello"})

​                db.stus.find({_id："Hello"})[0]              //是个数组    

​                

​                !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!拓展！！！！！！！！！！！！！！！！！！！！！！

​                db.stus.find({_id："Hello"})  表示的意思不是_id = "Hello"，而是 _id 有 "Hello"，_id可以是一个数组。

​                数组指包含，不是数组的指等于

​                同理：remove也一样

​                

​                !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!内嵌文档！！！！！！！！！！！！！！！！！！！！！！

​                stus ： {_id:11,username:"swk",hobby:{movies:["a","b","c"],cities:["d","e","f"]}}

​                现在查询movies有a的文档

​                db.stus.find({hobby.movies："a"})   此时报语法错误

​                如果通过内嵌文档来对文档进行查询，此时的属性名必须使用双引号或单引号

​                db.stus.find({"hobby.movies" ："a"})   意思是 hobby.movies不是某一个属性，而是一个表达式

​                现在给swk的电影加上一个"d"

​                db.stus.update({username:"swk"},{$set:{"hobby.movies" ："d"}})  这样直接把一个数组变成了一个字符串 $set是设置，

​                此时要找数组的update操作符：像数组中添加一个元素：  $push 或 $addToSet，区别在于 $addToSet会判断一下有没有重复，不会加重复的元素

​                db.stus.update({username:"swk"},{$push:{"hobby.movies" ："d"}})

​                

​                db.stus.find() 默认是按照_id排序，sal int类型

​                db.stus.find().sort({sal:1}) 按照sal升序

​                db.stus.find().sort({sal:-1}) 按照sal降序

​                db.stus.find().sort({sal:-1，empNum: 1}) 按照sal降序,empNum升序

​                

​                查询时只显示具体一列：第二个参数设置查询结果的投影,_ID默认下都有

​                db.stus.find({},{name : 1}).sort({sal:1})

​                _ID也省掉：

​                db.stus.find({},{name:1, _id:0}).sort({sal:1})

​                db.stus.find({},{name:true, _id:false}).sort({sal:1})  也对

​                

​            \- db.collection.findOne()

​                \- 查询第一个符合条件的文档

​                \- 返回的是一个对象

​                db.stus.findOne({_id："Hello"}).name   猪八戒

​            \- db.collection.find().count()

​              db.collection.find().length()

​                \- 查询符合条件的文档的数量

​                

​        \- 修改数据库中的文档

​            \- db.collection.update(查询条件，新对象)，默认下新对象会完全替换掉旧对象

​                                                      如果只是要修改指定属性，而不是替换，则需要使用修改操作符

​                                                      {<修改操作符>：{新对象}}

​                                                      默认情况下，如果查询条件匹配到多条数据，update只改一个。要修改全部:updateMany

​                                                      当然update也可以修改多个：.update(查询条件，新对象，{multe:true})

​                \- 可以修改、替换集合中的一个or多个文档

​                db.stus.update({name："沙和尚"},{age：28})，结果原来的沙和尚这个文档里就只剩下一个{age：28}这个属性了，其他的属性都没了。

​                db.stus.update({name："沙和尚"},{$set:{age：28}})，修改age这个属性，如果原来没有age属性，则添加之。

​                db.stus.update({name："沙和尚"},{$set:{age：28}},{multe: true})

​                db.stus.update({name："沙和尚"},{$unset:{age：28}})   $unset删除文档的指定属性，会把age属性删了。删文档用remove，删和添属性update

​                

​                找到年龄小于28的人，年龄加2

​                db.stus.updateMany({age:{$lt:28}},{$inc:{age:2}})

​                db.stus.updateMany({age:{$lt:28}},{$inc:{age:-2}})  减2

​            \- db.collection.updateOne()

​                \- 修改集合中的一个文档

​            \- db.collection.updateMany()

​                \- 修改集合中的多个文档

​            \- db.collection.replaceOne()

​                \- 替换集合中的一个文档

​                

​        \- 删除集合中的文档

​            \- db.collection.remove()    remove()必须传参：  .remove({})相当于全部删除数据， .remove()直接语法会报错

​                \- 删除集合中的一个或多个文档（默认删除多个）

​              db.collection.remove(查询条件,true)    则只删除一个

​            \- db.collection.deleteOne()

​                \- 删除集合中的一个文档

​            \- db.collection.deleteMany()

​                \- 删除集合中的多个文档

​            \- 清空一个集合（删除全部），性能差，一个一个删的，直接删集合就行了。用drop好

​                db.collection.remove({})

​            \- 删除一个集合，如果此集合是数据库里最后一个集合，则删除此集合，数据库也会删掉

​                db.collection.drop()

​            \- 删除一个数据库

​                db.dropDatabase()

​        \-  mongodb中的for 循环：  

​               插入2w条数据，执行了7.2 秒

​               for(var i=0; i<20000; i++) {

​                    db.stus.insert({name:i});

​               }

​               

​               优化： 执行了0.4秒，思想：数据库的方法能少就少

​               var arr = [];

​               for(var i=0; i<20000; i++) {

​                    arr.push({name:i});

​               }

​               db.stus.insert(arr);

​               

​               找name>500的文档：  db.stus.find({name ：{$gt : 500}})       $gt: > ;  $gte : >= ; $lt: < ;  $lte : <= ; $ne: !=  ;$eq: =

​               db.stus.find({name ：{$eq : 500}})  ==  db.stus.find({name ：500}),次场景下一样，如果是数组，就不一样了，数组下{name ：500}，指包含。

 

​               查看>40,<50的文档:

​               db.stus.find({name ：{$gt : 40, $lt : 50}})

​               

​               查看<40 或 >50的文档:

​               db.stus.find({$or : [{name ：{$gt : 40}}，{name ：{$lt : 50}}]})

​               

​               查看前10条数据的文档:  limit():显示数据的上限，就是用来分页的

​               db.stus.find().limit(10)

​               查看11到20条数据的文档： 分页第二页

​               db.stus.find().limit(11，20) 语法错误

​               db.stus.find().skip(10).limit(10)    .skip(10)跳过指定数量的数据  

​               查看21到30条数据的文档： 分页第3页

​               db.stus.find().skip(20).limit(10)    .skip(20)跳过指定数量的数据

​               在实际开发时，不会执行不带条件的查询。

​               分页：

​               .skip(页码-1 * 每页的条数).limit(每页的条数)  ==  .limit(每页的条数).skip(页码-1 * 每页的条数)

​               mongodb会自动调整limit和skip的位置

​               

​        \-  mongodb中 文档之间的关系：    

​               一对一， 一对多 多对一， 多对多        

​               一对一实际应用中较少，实现的话可以通过 内嵌文档的方式 实现：

​               insert({ name:"黄蓉"， huaband:{ name:"郭靖"} })    一对一

​               

​               一对多 多对一 实际应用中最多：

​               一对多：用户 订单，也可以用内嵌文档方式

​               方法1：insert({ name:"黄蓉"， dingdan:[{ name:"订单1"},{ name:"订单2"},{ name:"订单3"}]})

​               方法2： 1对多，这个多也要是唯一的对应一个人 , 在多的表里把一的那方设置为一个属性

​               db.users.insert([{user_id : "zhubajie"，user_name ："猪八戒"},{user_id : "sunwukong"，user_name ："孙悟空"}]);

​               

​               db.order.insert({list : ["牛肉","漫画"]，user_id : "zhubajie"});

​               db.order.insert({list : ["桃子","苹果"]，user_id : "sunwukong"});

​               现在查孙悟空的订单：

​               var id = db.users.findOne({user_name ："孙悟空"}).user_id;

​               db.order.findOne({user_id : id});

​               

​               多对多： 分类-商品

​               db.users.insert([{user_id : "zhubajie"，user_name ："猪八戒"},{user_id : "sunwukong"，user_name ："孙悟空"}]);

​               

​               db.order.insert({list : ["牛肉","漫画"]，user_id : ["zhubajie","sunwukong"]});

​               db.order.insert({list : ["桃子","苹果"]，user_id : ["zhubajie","sunwukong"]});

​               

4.js中使用mongodb ： Mongoose （尚硅谷）

通过程序来完成数据库的操作，Mongoose是通过Node来操作MongoDB，在nodeJs里编写程序来操作mongodb

​                   

​               

5.java中使用mongodb

准备: 驱动

​       mongo-java-driver-3.0.0.jar

查询一个collection下所有文档：              

//创建连接的客户端：

​    MongoClient client = new MongoClient(服务器IP,27017);

//获取数据库对象：

​    MongoDatabase db = client.getDataBase("myTest");     

//获取集合对象：               

​    MongoCollection<Document> collection = db.getCollection("users");     

//find操作：

​    FindIterable<Document> it = collection.find();

//获取游标对象

​    MongoCursor<Document> cursor = it.iterator();

​    while(cursor.hasNext()){

​        Document doc = cursor.next();

​    }

//释放资源

​    cursor.close();

​    client.close();

​    

查询一个collection下某一个文档:    

​    MongoClient client = new MongoClient(服务器IP,27017);

​    MongoDatabase db = client.getDataBase("myTest");     

​    MongoCollection<Document> collection = db.getCollection("users");

 

​    Bson filter = new BasicDBObject("_id",new ObjectId("1233333"));    

​    FindIterable<Document> it = collection.find(filter);

​    

​    MongoCursor<Document> cursor = it.iterator();

​    while(cursor.hasNext()){

​        Document doc = cursor.next();

​    }

​    cursor.close();

​    client.close();

​    

插入操作:    

​    MongoClient client = new MongoClient(服务器IP,27017);

​    MongoDatabase db = client.getDataBase("myTest");     

​    MongoCollection<Document> collection = db.getCollection("users");

​    Map m = new HashMap();

​    m.put(x,x);

​    Document doc = new Document(m);

​    collection.insertOne(doc);

​    client.close();

 

更新操作:

​    MongoClient client = new MongoClient(服务器IP,27017);

​    MongoDatabase db = client.getDataBase("myTest");     

​    MongoCollection<Document> collection = db.getCollection("users");

 

​    Bson filter = new BasicDBObject("_id",new ObjectId("1233333"));    

​    Map m = new HashMap();

​    m.put(x,x);

​    Bson update = new Bson(m);

​    collection.updateOneOne(filter, new BasicDBObject("$set",update));

​    client.close();

 

删除操作:

​    MongoClient client = new MongoClient(服务器IP,27017);

​    MongoDatabase db = client.getDataBase("myTest");     

​    MongoCollection<Document> collection = db.getCollection("users");    

​    collection.deleteOne(new BasicDBObject("_id",new ObjectId("1233333")));

​    client.close();

​    

===============================================================================SpringBoot==========================================================

SpringBoot的示例代码都托管在github中  Spring-Boot-Samples

 

架构演变：

   SpringBoot + SpringCloud + Spring Cloud Data Flow    

SpringBoot将应用打成可执行的jar包，直接使用java -jar的命令进行执行；不需要安装tomcat，其使用嵌入式的tomcat，所以其不支持JSP（war包），

可以使用模板引擎：thymeleaf

spring-boot-starter：spring-boot场景启动器    

Spring Boot将所有的功能场景都抽取出来，做成一个个的starters（启动器），只需要在项目里面引入这些starter相关场景的所有依赖都会导入进来    

\- resources文件夹中目录结构

  \- static：保存所有的静态资源； js css  images；

  \- templates：保存所有的模板页面；（Spring Boot默认jar包使用嵌入式的Tomcat，默认不支持JSP页面）；可以使用模板引擎（freemarker、thymeleaf）；

  \- application.properties：Spring Boot应用的配置文件；可以修改一些默认设置；

SpringBoot使用的全局的配置文件，！！！！配置文件名是固定的！！！！；application.properties   和   application.yml

配置文件的作用：修改SpringBoot自动配置的默认值；SpringBoot在底层都给我们自动配置好；

配置文件放在 /src/main/resources  或者 类路径/config 下

YAML：以数据为中心，比json、xml等更适合做配置文件,k:(空格)v：表示一对键值对（空格必须有）；以空格的缩进来控制层级关系；

只要是左对齐的一列数据，都是同一个层级的,属性和值也是大小写敏感；

yml语法：

1.字面量：普通的值（数字，字符串，布尔）

​    k: v：字面直接来写；

​        字符串默认不用加上单引号或者双引号；(application.properties也不需要引号)

​        ""：双引号；不会转义字符串里面的特殊字符；特殊字符会作为本身想表示的意思

​                name:   "zhangsan \n lisi"：输出；zhangsan 换行  lisi

​        ''：单引号；会转义特殊字符，特殊字符最终只是一个普通的字符串数据

​                name:   ‘zhangsan \n lisi’：输出；zhangsan \n  lisi

2.对象、Map（属性和值）（键值对）：

​    k: v：在下一行来写对象的属性和值的关系；注意缩进

​        对象还是k: v的方式

friends:

​        lastName: zhangsan

​        age: 20

行内写法： friends: {lastName: zhangsan,age: 18}        

3.数组（List、Set）：

用- 值表示数组中的一个元素

pets:

\- cat

\- dog

\- pig

 

行内写法： pets: [cat,dog,pig]

 

注解：

@SpringBootApplication 来标注一个主程序类，说明这是一个Spring Boot应用，标注main方法。@SpringBootApplication其实是@SpringBootConfiguration和@EnableAutoConfiguration

@SpringBootConfiguration  标注在某个类上，表示这是一个Spring Boot的配置类，其底层是@Configuration注解，是spring底层的注解。@Configuration

​            再点进去，他就是@Component,是一个组件。SpringBoot将配置文件替换成配置类

@EnableAutoConfiguration  开启自动配置功能；其底层： @AutoConfigurationPackage，

​                                            ！！！！！！！！其作用是：将主配置类（@SpringBootApplication标注的类）的所在包及下面所有子包里面的所有组件扫描到Spring容器，

​                                            所以如果@Controller写在其他包，不在@SpringBootApplication标注的类 的所在包及下面所有子包里面，则springBoot启动会失败！！！！

​                                                     @Import(EnableAutoConfigurationImportSelector.class)，Spring的底层注解@Import，给容器中导入一个组件，

​                                            其作用是告诉Spring要导哪些组件，将所有需要导入的组件以全类名的方式返回；这些组件就会被添加到容器中，再细一点：

​                                            会给容器中倒入非常多的自动配置类  XXXXAutoConfiguration，即所需要的组件，并配置好这些组件，这些自动配置类

​                                            都是写在一个配置文件中的：

​                                            ！！！！！！！！Spring Boot在启动的时候从类路径下的META-INF/spring.factories中

​                                            获取EnableAutoConfiguration指定的值，将这些值(xxxAutoConfiguration类)作为自动配置类导入到容器中，自动配置类就生效，帮我们进行自动配置工作！！！！

​                                            WebMvcAutoConfiguration.java  springMvc的自动配置

@Bean 给容器中添加一个组件。

 

@ConfigurationProperties： 告诉SpringBoot将本类中的所有属性和配置文件中相关的配置进行绑定，将配置文件中配置的每一个属性的值，映射到这个组件中

​                           prefix = "person"：配置文件中哪个下面的所有属性进行一一映射，只有这个组件是容器中的组件，才能容器提供的@ConfigurationProperties功能；

​                           @ConfigurationProperties(prefix = "person")默认从全局配置文件中获取值；

例子：  

@Component

@ConfigurationProperties(prefix = "person")

public class Person {

​    private String lastName;

​    private Integer age;

}

yml中：

person:

​    lastName: hello

​    age: 18

 

注入方法2： @Value: spring的底层注解，区别：@Value:只能获取基本类型，但是 ：@Value("${person.maps}") : 获取map等复杂类型会失效，@ConfigurationProperties不会失效。

@Component

public class Person {

​    @Value("${person.lastName}")

​    private String lastName;

​    @Value("#{11*2}")

​    private Integer age;

​    @Value("true")

​    private Boolean age;

}    

总结：

如果说，我们只是在某个业务逻辑中需要获取一下配置文件中的某项值，使用@Value；

如果说，我们专门编写了一个javaBean来和配置文件进行映射，我们就直接使用@ConfigurationProperties；

 

校验的注解：

@validated

@Component

public class Person {

​    @Value("${person.lastName}")

​    @Email

​    private String lastName;

}

 

springBoot单元测试： 可以在测试期间类似编码一样，自动注入

@RunWith(SpringRunner.class)  //springBoot的启动器，不用junit

@SpringBootTest    

 

@PropertySource：加载指定的配置文件；新建person.prioperties文件，将配置写到这个文件中，@PropertySource(value = {"classpath:person.prioperties"})

​                 @ConfigurationProperties(prefix = "person")默认从全局配置文件中获取值；

@Component

@PropertySource(value = {"classpath:person.prioperties"})

@ConfigurationProperties(prefix = "person")

public class Person {

​    private String lastName;

​    private Integer age;

}

 

SpringBoot与Spring配置文件整合：

@ImportResource：导入Spring的配置文件，让配置文件里面的内容生效；@ImportResource(locations = {"classpath:beans.xml"})

Spring Boot里面没有Spring的配置文件，我们自己编写的配置文件，也不能自动识别；

想让Spring的配置文件生效，加载进来；@ImportResource标注在一个配置类上

Spring配置文件 就是这个：  <bean>   </bean>

此方式不推荐,推荐使用全注解的方式

配置类@Configuration   代替 Spring配置文件，  <bean> == @Bean

！！！！！！！！！！！！！！！！@SpringBootConfiguration再系统启动时，会自动运行。类似于配置文件的自动加载。

@Configuration

public class MyConfig(){

​    

​    //将方法的返回值添加到容器中，容器中这个组件的ID，默认就是方法名,   <bean id="getXX" class="xx" />

​    @Bean

​    public xx getXX(){ sysout("execute getXX") }    //execute getXX 再网管启动时 会打印出来。

}

另一个类中：

@Autowired

ApplicationContext ioc;

 

ioc.containsBean("getXX");   true

 

 

 

Profile：

我们在主配置文件编写的时候，文件名可以是   application-{profile}.properties/yml

默认使用application.properties的配置；

方式一： 例如： 编写了2个配置文件

application-dev.properties     application-prod.properties

在主配置文件中： application.properties  配置文件中指定  spring.profiles.active=dev

方式二： yml文档块     ---标注 指明是另外一个文档了

在application.yml中 ：

server:

  port: 8081

spring:

  profiles:

​    active: prod

 

\---

server:

  port: 8083

spring:

  profiles: dev

 

 

\---

server:

  port: 8084

spring:

  profiles: prod  #指定属于哪个环境

  

  

配置文件加载位置：

springboot 启动会扫描以下位置的application.properties或者application.yml文件作为Spring boot的默认配置文件

–file:./config/       根目录

–file:./

–classpath:/config/    

–classpath:/

优先级由高到底，高优先级的配置会覆盖低优先级的配置； SpringBoot会从这四个位置全部加载主配置文件，！！！！！！！！！！互补配置！！！！！

也即： 高优先级覆盖部分内容，没有配置的用低优先级文件里的

 

 

SpringBoot自动配置原理： XXXXAutoConfiguration

以HttpEncodingAutoConfiguration（Http编码自动配置）为例解释自动配置原理；

 

@ConditionalOnXXX  //在指定条件成立的情况下自动配置类生效

​    例子：@ConditionalOnProperty(prefix = "spring.mvc", name = "data-format")

@Configuration   //表示这是一个配置类，以前编写的配置文件一样，也可以给容器中添加组件

@EnableConfigurationProperties(HttpEncodingProperties.class)  //启动指定类的ConfigurationProperties功能；将配置文件中对应的值和HttpEncodingProperties绑定起来；并把HttpEncodingProperties加入到ioc容器中

@ConditionalOnWebApplication //Spring底层@Conditional注解（Spring注解版），根据不同的条件，如果满足指定的条件，整个配置类里面的配置就会生效；    判断当前应用是否是web应用，如果是，当前配置类生效

@ConditionalOnClass(CharacterEncodingFilter.class)  //判断当前项目有没有这个类CharacterEncodingFilter；SpringMVC中进行乱码解决的过滤器；

@ConditionalOnProperty(prefix = "spring.http.encoding", value = "enabled", matchIfMissing = true)  //判断配置文件中是否存在某个配置  spring.http.encoding.enabled；如果不存在，判断也是成立的

//即使我们配置文件中不配置spring.http.encoding.enabled=true，也是默认生效的；

public class HttpEncodingAutoConfiguration {

  

​      //他已经和SpringBoot的配置文件映射了

​      private final HttpEncodingProperties properties;

  

   //只有一个有参构造器的情况下，参数的值就会从容器中拿

​      public HttpEncodingAutoConfiguration(HttpEncodingProperties properties) {

​        this.properties = properties;

​    }

  

​    @Bean   //给容器中添加一个组件，这个组件的某些值需要从properties中获取

​    @ConditionalOnMissingBean(CharacterEncodingFilter.class) //判断容器没有这个组件？

​    public CharacterEncodingFilter characterEncodingFilter() {

​        CharacterEncodingFilter filter = new OrderedCharacterEncodingFilter();

​        filter.setEncoding(this.properties.getCharset().name());

​        filter.setForceRequestEncoding(this.properties.shouldForce(Type.REQUEST));

​        filter.setForceResponseEncoding(this.properties.shouldForce(Type.RESPONSE));

​        return filter;

​    }

}

 

@ConfigurationProperties(prefix = "spring.http.encoding")  //从配置文件中获取指定的值和bean的属性进行绑定

public class HttpEncodingProperties {

   public static final Charset DEFAULT_CHARSET = Charset.forName("UTF-8");

}

 

 

！！！！！！！！！！！！！！！！！！！小结：

每一个XXXAutoConfiguration 都对应一个 XXXProperties 类。一旦XXXAutoConfiguration生效了，会给容器中添加各种组件：@Bean

这些组件的属性是从对应的XXXProperties类中获取的，这些类里面的每一个属性又是和配置文件绑定的；

 

 

**精髓：**

​    **1）、SpringBoot启动会加载main方法所在类，@EnableAutoConfiguration 会加载大量的自动配置类，在META-INF/spring.factories下

​    **2）、我们看我们需要的功能有没有SpringBoot默认写好的自动配置类；**

​    **3）、我们再来看这个自动配置类中到底配置了哪些组件；（只要我们要用的组件有，我们就不需要再来配置了）**

​    **4）、给容器中自动配置类添加组件的时候，会从XXXXproperties类中获取某些属性。我们就可以在配置文件中指定这些属性的值；**

 

xxxxAutoConfigurartion：自动配置类；给容器中添加组件: @bean

xxxxProperties:封装配置文件中相关属性；

 

 

 

SpringBoot日志：SpringBoot选用 SLF4j和logback；

给系统里面导入slf4j的jar和  logback的实现jar

SpringBoot默认帮我们配置好了日志；

 

​    Logger logger = LoggerFactory.getLogger(getClass());

​    @Test

​    public void contextLoads() {

​        //日志的级别；

​        //由低到高   trace<debug<info<warn<error

​        //可以调整输出的日志级别；日志就只会在这个级别以以后的高级别生效

​        logger.trace("这是trace日志...");

​        logger.debug("这是debug日志...");

​        //SpringBoot默认给我们使用的是info级别的，没有指定级别的就用SpringBoot默认规定的级别；root级别

​        logger.info("这是info日志...");

​        logger.warn("这是warn日志...");

​        logger.error("这是error日志...");

​    }

在application.properties中修改：

logging.level.包名=trace

logging.path=

\# 不指定路径在当前项目下生成springboot.log日志

\# 可以指定完整的路径；

logging.file=G:/springboot.log

 

\# 在当前磁盘的根路径下创建spring文件夹和里面的log文件夹；使用 spring.log 作为默认文件

logging.path=/spring/log

这2者是冲突的，默认是配置 logging.path

\# 指定文件中日志输出的格式

logging.pattern.file=%d{yyyy-MM-dd} === [%thread] === %-5level === %logger{50} ==== %msg%n

 

 

SpringBoot静态资源(html\css等)放在哪是有规定的：

所有 /webjars/** ，都去 classpath:/META-INF/resources/webjars/ 找资源；

webjars：以jar包的方式引入静态资源；

http://www.webjars.org/

以前是将jquery放在webapp下，页面上src引js，SpringBoot是用webjars的方式引,到官网上http://www.webjars.org/去找要引的(例如jquery的web-jar)对应的<dependency/>放到pom文件中.

例如: localhost:8080/webjars/jquery/3.3.1/jquery.js

类路径:

不要在 src 目录中放置除源代码之外的任何内容。

通常这里放入的文件都是 .java 文件。在有些情况下，也可放置 .html 文件（用于 JavaDoc）或其他类型的源代码。

然而，决不能在此结构内放置 .class 文件或任何其他编译并生成的工件

 

访问当前项目的任何资源，都去（静态资源的文件夹）找映射:

"classpath:/META-INF/resources/",

"classpath:/resources/",

"classpath:/static/",

"classpath:/public/"

"/"：当前项目的根路径

localhost:8080/abc ===  去静态资源文件夹里面找abc

 

欢迎页； 静态资源文件夹下的所有index.html页面；被"/**"映射；  localhost:8080/   找index页面

 

模板引擎:Thymeleaf

模板 + 数据模型 = 输出结果

1、引入thymeleaf；

​    去springBoot官网 或github 找Thymeleaf的starter，加到pom文件中

​        <dependency>

​            <groupId>org.springframework.boot</groupId>

​            <artifactId>spring-boot-starter-thymeleaf</artifactId>

​        </dependency>

​        

切换thymeleaf版本：  加到<properties>内

   <properties>

​        <thymeleaf.version>3.0.9.RELEASE</thymeleaf.version>

​        <!-- 布局功能的支持程序  thymeleaf3主程序  layout2以上版本 -->

​        <!-- thymeleaf2   layout1-->

​        <thymeleaf-layout-dialect.version>2.2.2</thymeleaf-layout-dialect.version>

   </properties>

 

2、Thymeleaf使用   ThymeleafAutoConfiguration  ===》 ThymeleafProperties

​    @ConfigurationProperties(prefix = "spring.thymeleaf")

​    public class ThymeleafProperties {

​         private static final Charset DEFAULT_ENCODING = Charset.forName("UTF-8");

​         private static final MimeType DEFAULT_CONTENT_TYPE = MimeType.valueOf("text/html");

​         public static final String DEFAULT_PREFIX = "classpath:/templates/";

​         public static final String DEFAULT_SUFFIX = ".html";

​    }

​    

​    只要我们把HTML页面放在classpath:/templates/，thymeleaf就能自动渲染；

 

3、Thymeleaf语法：

​    1)<html lang="en" xmlns:th="[http://www.thymeleaf.org](http://www.thymeleaf.org/)">  将xmlns加上去

​    2)      

​        后台向前台返回了一个Map<"hello"，"你好">

​        <!--th:text 将div里面的文本内容设置为 -->

        <div
th:text="${hello}">这是显示欢迎信息</div>   ${hello}会替换"这是显示欢迎信息"

 

​        th:text；改变当前元素里面的文本内容；

​        th：任意html属性；来替换原生属性的值，注意 是 替换

​        

​        th:insert  与 th:replace    类似于 jsp:include

​        th:each  类似于 jsp中 c:forEach

​        th:if th:unless :条件判断 c:if

​        th:attr  th:attrprepend  th:attrappend  : 任意属性修改

​        th:text；改变当前元素里面的文本内容，会转义特殊字符；    th:utext； 不转义特殊字符

​        th:fragment  ：声明片段

​        

​        hello: <h1>xx</h1>

​        th:text="${hello}"  结果：<h1>xx</h1>

​        th:utext="${hello}" 结果：xx  ，不转义 也就是 当成它的本意

​        

​        prods:数组

​        <tr th:each="prod : ${prods}">

​          <td th:text="${prod.name}"> xx </td>

​          <td th:text="${prod.age}"> xx </td>

​          <td th:text="${prod.isO}? #{true} #{false}"> xx </td>

​        </tr>

 

​        th:each每次遍历都会生成当前这个标签

​        <h4 th:text = "${prod.xx}"，th:each = "prod : ${prods}"> xx </h4>      会生成N个h4

​        <h5>

​            <span th:text = "${prod}"，th:each = "prod : ${prods}"> xx </span>   会生成1个h5,N个span

​        </h5>    

 

​        //行内写法：[[]] th:text 或者 [()] th:utext

​        <h5>

​            <span th:each = "prod : ${prods}"> [[${prod}]] </span>   会生成1个h5,N个span

​        </h5>

 

表达式语法：

​        ${...}：获取变量值   OGNL

​                ${person.father.name}

​                ${person['father']['name']}

​                ${person.functionA()}   ${person.functionA(xx)}  可以调用方法

​                

​                使用内置的基本对象：

​                     \#ctx : the context object.

​                     \#vars: the context variables.

​                     \#locale : the context locale.   区域信息

​                     \#request : (only in Web Contexts) the HttpServletRequest object.

​                     \#response : (only in Web Contexts) the HttpServletResponse object.

​                     \#session : (only in Web Contexts) the HttpSession object.

​                     \#servletContext : (only in Web Contexts) the ServletContext object.

​                ${#locale.country}    

​                

​                使用内置的一些工具对象：

​                     \#execInfo : information about the template being processed.

​                     \#messages : methods for obtaining externalized messages inside variables expressions, in the same way as they would be obtained using #{…} syntax.

​                     \#uris : methods for escaping parts of URLs/URIs

​                     \#conversions : methods for executing the configured conversion service (if any).

​                     \#dates : methods for java.util.Date objects: formatting, component extraction, etc.

​                     \#calendars : analogous to #dates , but for java.util.Calendar objects.

​                     \#numbers : methods for formatting numeric objects.

​                     \#strings : methods for String objects: contains, startsWith, prepending/appending, etc.

​                     \#objects : methods for objects in general.

​                     \#bools : methods for boolean evaluation.

​                     \#arrays : methods for arrays.

​                     \#lists : methods for lists.

​                     \#sets : methods for sets.

​                     \#maps : methods for maps.

​                     \#aggregates : methods for creating aggregates on arrays or collections.

​                     \#ids : methods for dealing with id attributes that might be repeated (for example, as a result of an iteration).

​                ${#strings.toString(obj)}      ${#strings.isEmpty(obj)}     ${#strings.contains(name,'ez')}

​                ${#strings.trim(name)}        ${#strings.length(name)}

​                

​        *{...}：选择表达式：和${}在功能上是一样；不同之处：配合 th:object="${session.user}：

                 <div
th:object="${session.user}">

                     <p>Name:
<span
th:text="*{firstName}">Sebastian</span>.</p>               //*

就代表 th:object，类似于 <p>Name: <span
th:text="${session.user.firstName}">Sebastian</span>.</p>

                     <p>Surname:
<span th:text="*{lastName}">Pepper</span>.</p>

                     <p>Nationality:
<span th:text="*{nationality}">Saturn</span>.</p>

​                 </div>

​        \#{...}：获取国际化内容

​        @{...}：定义URL；

             <a
href="a.html" th:href = "@{http://localhost:8080/order(orderId=${o.id},orderType='FAST')}">view</a>

​             th:xx 起替换作用，以前的变量：  http://localhost:8080/order?orderId=4

             <a
href="a.html" th:href =
"@{/order(orderId=${o.id},orderType='FAST')}">view</a>  就代表当前项目下

​             th:href = "@{/order} + ${xx.xx}"   2种标签不能写在一起

​            

​            

​             @{...}：里 /order？orderId=${o.id}   ===》 @{/order(orderId=${o.id}) ,用小括号表示参数

​        ~{...}：片段引用表达式

             <div
th:insert="~{commons :: main}">...</div>

 

​        th:attr = "src = ${},title = ${}"

SpringBoot整合springMvc

springMvc复习下：

springMvc：所有的请求最终==》 DispatcherServlet(web.xml)的doDispatch(HttpServletRequest request,HttpServletReponse response)方法来处理@controller方法返回的结果。

springMvc的配置文件： springmvc.xml中配置了 拦截器，视图映射，视图解析器（ViewResolver） 等，配置DispatcherServlet时会把springmvc.xml也传进去。DispatcherServlet有个init-param

叫ContextConfigLocation，就是springmvc.xml的位置信息。

 

@RequestMapping(value="/users")还有一个常用的属性： method=RequestMethod.POST, REST风格的url请求。

url： a/b/1

@RequestMapping(value="/a/b/{id}" method=RequestMethod.POST)    

public void e(@PathVariable("id") Integer id){}

 

如果不是rest风格url：

url： a/b?name = xx & age = xx  

@RequestMapping(value="/a/b")

public void e(@RequestParam("name") String name, @RequestParam("age") Integer age){}

 

当属性较多时，可以不用@RequestParam，直接用一个对象来接受参数，springmvc会将请求参数名，与pojo属性名进行自动匹配，自动为该对象填充属性名。

url： a/b

@RequestMapping(value="/a/b")

public void e(User user){}

 

！！！！！！！！！！！！！重要：SpringMVC的Handler方法可以使用servlet原生的API作为目标方法的参数，具体支持以下类型：

\* HttpServletRequest   * HttpServletResponse  * HttpSession   * java.security.Principal

\* Locale     InputStream(请求的HttpServletRequest.getInputStream)   * OutputStream(响应的HttpServletResponse.getOutputStream)          * Reader(请求的HttpServletRequest.getReader)        * Writer(响应的Writer)

此时，需要在pom.xml增加如下配置（别忘了版本<servlet-api.version>3.1.0</servlet-api.version>）：

​         <dependency>

​             <groupId>javax.servlet</groupId>

​             <artifactId>javax.servlet-api</artifactId>

​             <version>${servlet-api.version}</version>

​             <scope>provided</scope>

​         </dependency>

  @Controller

  public class SpringMVCTest {

​      private static final String SUCCESS = "success";

​      @RequestMapping("/testServletAPI")

​      public void testServletAPI(HttpServletRequest request,HttpServletResponse response,Writer out) throws IOException {

​          System.out.println("testServletAPI," + request + "," + response);

​          out.write("hello");

  }

  在页面中会打印出hello

 

在不加@reponseBody标签时，controller返回值通常解析为跳转路径，无论我们的controller返回的是一个String、ModelAndView、Model ，DispatcherServlet都会将他转化为一个ModelAndView

SpringMvc返回值给servlet，jsp如何取到这个值呢？

===》 SpringMvc会将 @Controller方法返回的ModelAndView中的model、  @Controller方法传参的Map、Model类型，自动的加入到request域中。（SpringMvc在调用方法前会

创建一个隐含的模型对象作为存储容器）

  @Controller

  public class SpringMVCTest {

​      private static final String SUCCESS = "success";

​      @RequestMapping("/testServletAPI")

​      public void testServletAPI(HttpServletRequest request,HttpServletResponse response,Writer out,Map<String,Object> map) throws IOException {

​          System.out.println("testServletAPI," + request + "," + response);

​          map.put("a",new Object());

​          out.write("hello");

  }

  jsp中 ${requestScope.a}

  

  @Controller

  public class SpringMVCTest {

​      private static final String SUCCESS = "success";

​      @RequestMapping("/testServletAPI")

​      public ModelAndView testServletAPI(HttpServletRequest request,HttpServletResponse response,Writer out) throws IOException {

​          System.out.println("testServletAPI," + request + "," + response);

​          map.put("a",new Object());

​          out.write("hello");

​          

​          ModelAndView modekandview = new ModelAndView("success");  success: view视图名

​          modekandview.addObject("a",new Object());

​          return modekandview;

  }

  jsp中 ${requestScope.a}

  

如要多个请求公用某个对象，在Controller的类上加上 @SessionAttribute，SpringMvc会将次对象放到httpSession中

  @Controller

  @SessionAttribute(value = {"user"} , type = {String.class})   //并集关系

  public class SpringMVCTest {

​      @RequestMapping("/testServletAPI")

​      public String testServletAPI(HttpServletRequest request,HttpServletResponse response,Writer out，Map<String,Object> map) throws IOException {

​          System.out.println("testServletAPI," + request + "," + response);

​          map.put("a",new Object(););

​          out.write("hello");

 

​          User user = new User();

​          map.put("user",user);

​          map.put("aa",new Object());

  }

则Session中： 会有 user 和 aa

 

视图解析器：根据方法的返回值得到视图对象（View），视图对象决定如何渲染（转发？重定向？））

public interface View(){

​    public String getContentType();

​    

​    public void render();

}

 

@responsebody 注解

表示该方法的返回结果直接写入HTTP response body中。

1、一般在异步获取数据时使用，在使用@RequestMapping后，返回值通常解析为跳转路径，

加上@responsebody后返回结果不会被解析为跳转路径，

而是直接写入HTTP response body中。比如异步获取json数据，加上@responsebody后，会直接返回json数据。

 

@Controller

@RequestMapping("/")

public class HelloController {

@RequestMapping(value = "/something", method = RequestMethod.GET)

@ResponseBody

public String helloWorld() {

return"Hello World";

}

}

运行以上代码，在浏览器地址栏输入： http://localhost:8080/something

运行结果，页面上输出 Hello World

结果表明：如果在一个方法上使用了@RequestMapping注解，这时候，方法的返回值通常解析为跳转的路径， 也就是说，要跳转到指定的jsp页面。

在这个代码实例中，要跳转到的是 Hello World.jsp 页面。 因为工程中尚未添加这个jsp文件，所以报出了 404 错误 （The requested resource is not available）。

如果添加了 @ResponseBody搜索 这个注解， 则表明该方法的返回值直接写入到 HTTP Response Body 中。

这就是说，如果返回的是JSON， 就得必须添加 @ResponseBody 这个注解

一般在异步获取数据时使用，在使用@RequestMapping后，

返回值通常解析为跳转路径，加上@responsebody后返回结果不会被解析为跳转路径，

而是直接写入HTTP response body中。比如异步获取json数据，加上@responsebody后，会直接返回json数据。

 

ajax + @ResponseBody + JSON 的方式 用来controller返回一个对象，前台解析为一个json。

 

 

@RestController

@RequestMapping(value="/users")

public class MyRestController {

​    @RequestMapping(value="/{user}", method=RequestMethod.GET)

​    public User getUser(@PathVariable Long user) {

​        // ...

​    }

 

​    @RequestMapping(value="/{user}/customers", method=RequestMethod.GET)

​    List<Customer> getUserCustomers(@PathVariable Long user) {

​        // ...

​    }

 

​    @RequestMapping(value="/{user}", method=RequestMethod.DELETE)

​    public User deleteUser(@PathVariable Long user) {

​        // ...

​    }

}            

SpringBoot对SpringMVC的默认配置：   webMvcAutoConfiguration

​    自动配置了ViewResolver（视图解析器：根据方法的返回值得到视图对象（View），视图对象决定如何渲染（转发？重定向？））    

 

SpringBoot拓展SpringMvc（页面跳转不需要写一些空方法）

//使用WebMvcConfigurerAdapter可以来扩展SpringMVC的功能，为什么能拓展，就是因为原来自动配置的有个注解：@ConditionalOnMissingBean，容器中没有用户自己配的，就用这个

//@EnableWebMvc   不要接管SpringMVC

@Configuration

public class MyMvcConfig extends WebMvcConfigurerAdapter {

 

​    @Override

​    public void addViewControllers(ViewControllerRegistry registry) {

​        //super.addViewControllers(registry);

​        //浏览器发送 /atguigu 请求来到 success

​        //添加视图映射

​        registry.addViewController("/atguigu").setViewName("success");

​    }

 

​    //所有的WebMvcConfigurerAdapter组件都会一起起作用

​    @Bean //将组件注册在容器

​    public WebMvcConfigurerAdapter webMvcConfigurerAdapter(){

​        WebMvcConfigurerAdapter adapter = new WebMvcConfigurerAdapter() {

​            @Override

​            public void addViewControllers(ViewControllerRegistry registry) {

​                registry.addViewController("/").setViewName("login");

​                registry.addViewController("/index.html").setViewName("login");

​            }

​        };

​        return adapter;

​    }

}    

 

Themeleaf中：controller中依旧要返回再给前台消息怎么办？

和springMvc一样，可以在controller的方法中加一个Map或Model，Map.put("key","xx") Model.addAttribute("key","xx") 这个Map都不需要返回，自己加到request域中。

前台：  ${key}

th:if  高优先级的,如果th:if 不满足，则th:text = "${key}"不显示，p标签也不会生成

<p th:text = "${key}"  th:if
="$(not #strings.isEmpty(key))"></p>

 

Themeleaf  ： Template Layout

​    th:fragment="xxx" 要抽取的片段

      <div
th:fragment="copy">

​         &copy; 2011 The Good Thymes Virtual Grocery

​      </div>

​    th:insert="~{xx}" 或者： th:insert="xx"  将要抽取的插入进来

​    th:include

​    th:replace

      <div th:insert="~{footer
:: copy}"></div>

​      ~{templatename::selector}：模板名::选择器

​      ~{templatename::fragmentname}:模板名::片段名

​      模板名会使用Themeleaf的前后缀配置规则来进行解析。

​      在A.html中：

      <div
th:fragment="copy">   &copy; 2011 The Good
Thymes Virtual Grocery  </div>

​      在B.html

      <div
th:insert="~{A::copy}">  </div>  //~{templatename::fragmentname}

​      

​      or：

​      在A.html中：

      <div
id="fff">   &copy; 2011 The Good Thymes Virtual
Grocery  </div>

​      在B.html

      <div th:insert="~{A::#fff}">  </div>  //~{templatename::selector}

​      

​      

​      

​    三种引入公共片段的th属性：

 

**th:insert**：将公共片段整个插入到声明引入的元素（div）中

**th:replace**：将声明引入的元素替换为公共片段

**th:include**：将被引入的片段的内容包含进这个标签中

 

\```html

<footer th:fragment="copy">

&copy; 2011 The Good Thymes Virtual Grocery

</footer>

 

引入方式

<div th:insert="footer ::
copy"></div>

<div th:replace="footer ::
copy"></div>

<div th:include="footer ::
copy"></div>

 

效果

<div>

​    <footer>

​    &copy; 2011 The Good Thymes Virtual Grocery

​    </footer>

</div>

 

<footer>

&copy; 2011 The Good Thymes Virtual Grocery

</footer>

 

<div>

&copy; 2011 The Good Thymes Virtual Grocery

</div>

 

被引入片段的时候传入参数：

<div
th:replace="commons/bar::#sidebar(activeUri='emps')"></div>

引入片段html中：

<a class="nav-link active"

​    th:class="${activeUri=='main.html'?'nav-link active':'nav-link'}"

​    href="#" th:href="@{/main.html}">

​        

 

SpringBoot配置嵌入式servlet：

以前： web应用打成war包，放入到外部的tomcat环境，tomcat环境就是一个servlet容器

 

 

如何修改SpringBoot的默认配置

模式：

​    1）SpringBoot在自动配置很多组件的时候，先看容器中有没有用户自己配置的（@Bean、@Component）如果有就用用户配置的，如果没有，才自动配置；

如果有些组件可以有多个（ViewResolver）将用户配置的和自己默认的组合起来；

​    2）在SpringBoot中会有非常多的xxxConfigurer帮助我们进行扩展配置

​    3）在SpringBoot中会有很多的xxxCustomizer帮助我们进行定制配置

 

由于SpringBoot默认是以jar包的方式启动嵌入式的Servlet容器来启动SpringBoot的web应用，没有web.xml文件。

SpringBoot没有 src/webApp/web.xml这些配置

SpringBoot要注册Servlet三大组件【Servlet、Filter、Listener】怎么办？

没有配置文件，那肯定用配置类：

 

@Configuration

public class MyServerConfig(){

​    //ServletRegistrationBean

​    @Bean

​    public ServletRegistrationBean myServlet(){

​         ServletRegistrationBean registrationBean = new ServletRegistrationBean(new MyServlet(),"/myServlet");  //MyServlet是自定义的Servlet，extends HttpServlet，实现doGet doPost方法

​         return registrationBean;

​    }

}

import javax.servlet.Filter;

public class MyFilter extends Filter{

​    init  doFilter  destory

}

@Bean

public FilterRegistrationBean myFilter(){

​    FilterRegistrationBean registrationBean = new FilterRegistrationBean();

​    registrationBean.setFilter(new MyFilter());

​    registrationBean.setUrlPatterns(Arrays.asList("/hello","/myServlet"));

​    return registrationBean;

}

 

@Bean

public ServletListenerRegistrationBean myListener(){

​    ServletListenerRegistrationBean<MyListener> registrationBean = new ServletListenerRegistrationBean<>(new MyListener());

​    return registrationBean;

}

 

 

SpringBoot帮我们自动SpringMVC的时候，自动的注册SpringMVC的前端控制器；DIspatcherServlet；

DispatcherServletAutoConfiguration中：

 

@Bean(name = DEFAULT_DISPATCHER_SERVLET_REGISTRATION_BEAN_NAME)

@ConditionalOnBean(value = DispatcherServlet.class, name = DEFAULT_DISPATCHER_SERVLET_BEAN_NAME)

public ServletRegistrationBean dispatcherServletRegistration(

​      DispatcherServlet dispatcherServlet) {

   ServletRegistrationBean registration = new ServletRegistrationBean(

​         dispatcherServlet, this.serverProperties.getServletMapping());

​    !!!!!!!!!!!!!!!!!!!!!!//默认拦截： /  所有请求；包静态资源，但是不拦截jsp请求；   /*会拦截jsp  !!!!!!!!!!!!!!!!!!!!!!!!!!!

​    //可以通过server.servletPath来修改SpringMVC前端控制器默认拦截的请求路径

​    

   registration.setName(DEFAULT_DISPATCHER_SERVLET_BEAN_NAME);

   registration.setLoadOnStartup(

​         this.webMvcProperties.getServlet().getLoadOnStartup());

   if (this.multipartConfig != null) {

​      registration.setMultipartConfig(this.multipartConfig);

   }

   return registration;

}

 

 

2）、SpringBoot能支持其他的Servlet容器；jetty(适合长连接，比如web聊天，双方一直架着连接)

​                                        undertow(不支持jsp，适合高并发)

​                                        

​                                        

使用外置的Servlet容器：

嵌入式Servlet容器：应用打成可执行的jar

​        优点：简单、便携；

​        缺点：默认不支持JSP、优化定制比较复杂（使用定制器【ServerProperties、自定义EmbeddedServletContainerCustomizer】，自己编写嵌入式Servlet容器的创建工厂【EmbeddedServletContainerFactory】）；

外置的Servlet容器：外面安装Tomcat---应用war包的方式打包；

\### 步骤

1）、必须创建一个war项目；（利用idea创建好目录结构）

2）、将嵌入式的Tomcat指定为provided；

\```xml

<dependency>

   <groupId>org.springframework.boot</groupId>

   <artifactId>spring-boot-starter-tomcat</artifactId>

   <scope>provided</scope>

</dependency>

\```

3）、必须编写一个**SpringBootServletInitializer**的子类，并调用configure方法

\```java

public class ServletInitializer extends SpringBootServletInitializer {

   @Override

   protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {

​       //传入SpringBoot应用的主程序

​      return application.sources(SpringBoot04WebJspApplication.class);

   }

}

\```

4）、启动服务器就可以使用；

\### 原理

jar包：执行SpringBoot主类的main方法，启动ioc容器，创建嵌入式的Servlet容器；

war包：启动服务器，**服务器启动SpringBoot应用**【SpringBootServletInitializer】，启动ioc容器；

 

 

\#SpringBoot与数据访问

无论是SQL和NoSQL,SpringBoot采用整合Spring Data的方式进行统一处理。引入 xxxTemplate、xxxRepository来操作数据库。

整合MyBatis

\```xml

​        <dependency>

​            <groupId>org.mybatis.spring.boot</groupId>

​            <artifactId>mybatis-spring-boot-starter</artifactId>

​            <version>1.3.1</version>

​        </dependency>

 

1）、注解版

//指定这是一个操作数据库的mapper

@Mapper

public interface DepartmentMapper {

​    @Select("select * from department where id=#{id}")

​    public Department getDeptById(Integer id);

 

​    @Delete("delete from department where id=#{id}")

​    public int deleteDeptById(Integer id);

 

​    @Options(useGeneratedKeys = true,keyProperty = "id")

​    @Insert("insert into department(departmentName) values(#{departmentName})")

​    public int insertDept(Department department);

 

​    @Update("update department set departmentName=#{departmentName} where id=#{id}")

​    public int updateDept(Department department);

}

MybatisAutoConfiguration.java

xxxCustomizer；用来定制的

自定义MyBatis的配置规则；给容器中添加一个ConfigurationCustomizer；

@org.springframework.context.annotation.Configuration

public class MyBatisConfig {

​    @Bean

​    public ConfigurationCustomizer configurationCustomizer(){

​        return new ConfigurationCustomizer(){

​            @Override

​            public void customize(Configuration configuration) {

​                configuration.setMapUnderscoreToCamelCase(true);

​            }

​        };

​    }

}

 

或者Mapper类上不加@Mapper注解

使用MapperScan批量扫描所有的Mapper接口；

@MapperScan(value = "com.atguigu.springboot.mapper")

@SpringBootApplication

public class SpringBoot06DataMybatisApplication {

​    public static void main(String[] args) {

​        SpringApplication.run(SpringBoot06DataMybatisApplication.class, args);

​    }

}

 

2）、配置文件的方式

去GitHub中搜索mybatis 配置全局配置文件<environment>  <mapper>、 SQL映射文件

\```yaml

mybatis:

  config-location: classpath:mybatis/mybatis-config.xml 指定全局配置文件的位置

  mapper-locations: classpath:mybatis/mapper/*.xml  指定sql映射文件的位置

 

SQL映射文件：

<mapper namespace="mapper类的全类名" >

​    <select id="xxx" resultType="yyy">  

​    </select>

</mapper>

xxx就是mapper类中的方法名字。resultType方法返回的类型

 

SpringBoot与缓存

1.开启基于注解的缓存  在启动类上 @EnableCaching

2.标注缓存注解  @Cacheable @CacheEvict @CachePut @Caching

 

@Cacheable标注的方法执行之前先来检查缓存中有没有这个数据，默认按照参数的值作为key去查询缓存，

如果没有就运行方法并将结果放入缓存；以后再来调用就可以直接使用缓存中的数据；

原理：

​     \*   1、自动配置类；CacheAutoConfiguration

​     \*   2、缓存的配置类

​     \*   org.springframework.boot.autoconfigure.cache.GenericCacheConfiguration

​     \*   org.springframework.boot.autoconfigure.cache.JCacheCacheConfiguration

​     \*   org.springframework.boot.autoconfigure.cache.EhCacheCacheConfiguration

​     \*   org.springframework.boot.autoconfigure.cache.HazelcastCacheConfiguration

​     \*   org.springframework.boot.autoconfigure.cache.InfinispanCacheConfiguration

​     \*   org.springframework.boot.autoconfigure.cache.CouchbaseCacheConfiguration

​     \*   org.springframework.boot.autoconfigure.cache.RedisCacheConfiguration

​     \*   org.springframework.boot.autoconfigure.cache.CaffeineCacheConfiguration

​     \*   org.springframework.boot.autoconfigure.cache.GuavaCacheConfiguration

​     \*   org.springframework.boot.autoconfigure.cache.SimpleCacheConfiguration【默认】

​     \*   org.springframework.boot.autoconfigure.cache.NoOpCacheConfiguration

​     \*   3、哪个配置类默认生效：SimpleCacheConfiguration；

​     \*   4、给容器中注册了一个CacheManager：ConcurrentMapCacheManager

​     \*   5、可以获取和创建ConcurrentMapCache类型的缓存组件；他的作用将数据保存在ConcurrentMap中；(不用redis，redis与之相比最大的区别，redis可以持久化)

几个属性：

​     \*      cacheNames/value：指定缓存组件的名字;将方法的返回结果放在哪个缓存中，是数组的方式，可以指定多个缓存；

​     \*      key：缓存数据使用的key；可以用它来指定。默认是使用方法实参的值，如果ID传来是1，  1-方法的返回值放到缓存中

​     \*              编写SpEL； #id;参数id的值   #a0  #p0  #root.args[0]

​     \*              默认：@Cacheable(value = {"emp"},key = "#id") ==> @Cacheable(value = {"emp"},key = "#root.args[0]")

​                          @Cacheable(value = {"emp1","tempemp2"},key = "#id") 2个缓存, root.caches[0].name

​     \*              去Cache中查找缓存的内容，使用一个key，默认就是方法的参数；

​     \*              key是按照某种策略生成的；默认是使用keyGenerator生成的，默认使用SimpleKeyGenerator生成key；

​     \*              SimpleKeyGenerator生成key的默认策略；

​     \*                  如果没有参数；key=new SimpleKey()；

​     \*                  如果有一个参数：key=参数的值

​     \*                  如果有多个参数：key=new SimpleKey(params)；      //多个参数属性封装成一个对象                  

​     \*      keyGenerator：key的生成器；可以自己指定key的生成器的组件id

​     \*              key/keyGenerator：二选一使用;

​     \*      cacheManager：指定缓存管理器；或者cacheResolver指定获取解析器

​     \*      condition：指定符合条件的情况下才缓存；

​     \*          condition = "#id>0"

​     \*          condition = "#a0>1"：第一个参数的值》1的时候才进行缓存

​     \*      unless:否定缓存；当unless指定的条件为true，方法的返回值就不会被缓存；可以获取到结果进行判断

​     \*              unless = "#result == null"                #result表示返回的结果。

​     \*              unless = "#a0==2":如果第一个参数的值是2，结果不缓存；

​     \*      sync：是否使用异步模式，默认是方法执行完以同步的方式 将结果放入到缓存中。

核心：

​     \*      1）、使用CacheManager【ConcurrentMapCacheManager】按照名字得到Cache【ConcurrentMapCache】组件

​     \*      2）、key使用keyGenerator生成的，默认是SimpleKeyGenerator

​    

@Cacheable(value = {"emp"},keyGenerator = "myKeyGenerator",condition = "#a0>1",unless = "#a0==2")

public Employee getEmp(Integer id){

​    System.out.println("查询"+id+"号员工");

​    Employee emp = employeeMapper.getEmpById(id);

​    return emp;

}

如果想用自定义的keyGenerator：

@Configuration

public class MyCacheConfig {

​    @Bean("myKeyGenerator")   //默认的bean ID 是 keyGenerator，可以改名字。

​    public KeyGenerator keyGenerator(){

​        return new KeyGenerator(){

​            @Override

​            public Object generate(Object target, Method method, Object... params) {

​                return method.getName()+"["+ Arrays.asList(params).toString()+"]";

​            }

​        };

​    }

}

自己的总结：无论什么时候@Cacheable都是先从缓存中取数据，如果缓存中没有，则查询数据库，再放入缓存中。

 

 

@CachePut：既调用方法，又更新缓存数据；同步更新缓存，

此方法不被推荐：高并发下会有问题。低并发下没问题

比如A，B同时进行更新操作：1.A更新数据库   2.B更新数据库   3.B更新缓存    4.A更新缓存  正确的应该是A先更新缓存

比如：在写数据库场景比较多的，而读数据库比较少的情况下，缓存被频繁的修改，浪费性能，直接删除缓存更好

\* 运行时机：

​     \*  1、先调用目标方法

​     \*  2、将目标方法的结果缓存起来

​     \* 测试步骤：

​     \*  1、查询1号员工；查到的结果会放在缓存中；

​     \*          key：1  value：lastName：张三

​     \*  2、以后查询还是之前的结果

​     \*  3、更新1号员工；【lastName:zhangsan；gender:0】

​     \*     将方法的返回值也放进缓存了；

​     \*     key：传入的employee对象  值：返回的employee对象；

​     \*  4、查询1号员工？

​     \*      应该是更新后的员工；

​     \*          key = "#employee.id":使用传入的参数的员工id；

​     \*          key = "#result.id"：使用返回后的id

​     \*          @Cacheable的key是不能用#result

​     \*      为什么是没更新前的？【1号员工没有在缓存中更新】

​     */

@CachePut(value = "emp",key = "#result.id")

public Employee updateEmp(Employee employee){

​     System.out.println("updateEmp:"+employee);

​     employeeMapper.updateEmp(employee);

​     return employee;

}

注： 取缓存的key和放缓存的key一定要一样

 

@CacheEvict：缓存清除

​     \*  key：指定要清除的数据

​     \*  allEntries = true：指定清除这个缓存中所有的数据

​     \*  beforeInvocation = false：缓存的清除是否在方法之前执行

​     \*      默认代表缓存清除操作是在方法执行之后执行;如果出现异常缓存就不会清除

​     *

​     \*  beforeInvocation = true：

​     \*      代表清除缓存操作是在方法运行之前执行，无论方法是否出现异常，缓存都清除

​     */

​    @CacheEvict(value="emp",beforeInvocation = true/*key = "#id",*/)

​    public void deleteEmp(Integer id){

​        System.out.println("deleteEmp:"+id);

​        //employeeMapper.deleteEmpById(id);

​        int i = 10/0;

​    }

 

@Caching：定义复杂的缓存规则

​    @Caching(

​         cacheable = {

​             @Cacheable(/*value="emp",*/key = "#lastName")

​         },

​         put = {

​             @CachePut(/*value="emp",*/key = "#result.id"),

​             @CachePut(/*value="emp",*/key = "#result.email")

​         }

​    )

​    public Employee getEmpByLastName(String lastName){

​        return employeeMapper.getEmpByLastName(lastName);

​    }

 

 

​    

或者直接在整个类上： @CacheConfig(value ="emp"),下面的各个方法就不需要value="emp"。//抽取缓存的公共配置

 

SpringBoot整合Redis

1.pom文件中倒入redis的starter  ----  RedisAutoConfiguration: 加了这样的组件：

​                      RedisTemplate<Object,Object>：操作KV都是对象的   StringRedisTemplate：操作KV都是字符串的(类似于JdbcTemplate操作数据库一样)  

2.在全局配置文件中，配上redis主机地址：spring.redis.host

3.在service方法中：

  @Autowired

  StringRedisTemplate stringRedisTemplate;

\*  stringRedisTemplate.opsForValue()[String（字符串）]

\*  stringRedisTemplate.opsForList()[List（列表）]

\*  stringRedisTemplate.opsForSet()[Set（集合）]

\*  stringRedisTemplate.opsForHash()[Hash（散列）]

\*  stringRedisTemplate.opsForZSet()[ZSet（有序集合）]

 

stringRedisTemplate.opsForValue().append(String key,String Value)

stringRedisTemplate.opsForValue().muitiSet(Map<String,String>)

stringRedisTemplate.opsForValue().get(String key)

stringRedisTemplate.opsForList().leftPush("myList","1");

 

方法2：

由RedisCacheManager===>Cache，通过Cache操作缓存。

 

 

Employee empById = employeeMapper.getEmpById(1);

//默认如果保存对象，使用jdk序列化机制，序列化后的数据保存到redis中

Employee这个类要序列化。 implements Serializable

redisTemplate.opsForValue().set("emp-01",empById);  //序列化后的结果：机器看懂，所以要用json的方式

//1、将数据以json的方式保存

//(1)自己将对象转为json

//(2)redisTemplate默认的序列化规则；改变默认的序列化规则；

@AutoWired

RedisTemplate<Object, Employee> empRedisTemplate;

empRedisTemplate.opsForValue().set("emp-01",empById);

 

@Configuration

public class MyRedisConfig {

​    @Bean

​    public RedisTemplate<Object, Employee> empRedisTemplate(

​            RedisConnectionFactory redisConnectionFactory)

​            throws UnknownHostException {

​        RedisTemplate<Object, Employee> template = new RedisTemplate<Object, Employee>();

​        template.setConnectionFactory(redisConnectionFactory);

​        Jackson2JsonRedisSerializer<Employee> ser = new Jackson2JsonRedisSerializer<Employee>(Employee.class);

​        template.setDefaultSerializer(ser);

​        return template;

​    }

}

这个Bean，empRedisTemplate就是bean的ID，大部分是直接拷贝的源代码，

Jackson2JsonRedisSerializer<Employee> ser = new Jackson2JsonRedisSerializer<Employee>(Employee.class);

template.setDefaultSerializer(ser);  是自己加的

 

这样的话，到redis中去看，存放的就是json了。

 

步骤：

1、引入了redis的starter，cacheManager变为 RedisCacheManager；

2、默认创建的 RedisCacheManager 操作redis的时候使用的是 RedisTemplate<Object, Object>  方法2： RedisCacheManager===>Cache

​        Cache dept = deptCacheManager.getCache("dept");

​        dept.put("dept:1",department);

3、RedisTemplate<Object, Object> 是 默认使用jdk的序列化机制

原理：CacheManager===>Cache 缓存组件来实际给缓存中存取数据

====》  自定义CacheManager

​    @Primary  //将某个缓存管理器作为默认的

​    @Bean

​    public RedisCacheManager employeeCacheManager(RedisTemplate<Object, Employee> empRedisTemplate){   //empRedisTemplate 9690行被注入进来了

​        RedisCacheManager cacheManager = new RedisCacheManager(empRedisTemplate);

​        //key多了一个前缀

​        //使用前缀，默认会将CacheName作为key的前缀

​        cacheManager.setUsePrefix(true);

​        return cacheManager;

​    }

 

​    @Bean

​    public RedisCacheManager deptCacheManager(RedisTemplate<Object, Department> deptRedisTemplate){

​        RedisCacheManager cacheManager = new RedisCacheManager(deptRedisTemplate);

​        //key多了一个前缀

​        //使用前缀，默认会将CacheName作为key的前缀

​        cacheManager.setUsePrefix(true);

​        return cacheManager;

​    }

 

@Service

public class DeptService {

​    @Autowired

​    DepartmentMapper departmentMapper;

 

​    @Qualifier("deptCacheManager")

​    @Autowired

​    RedisCacheManager deptCacheManager;

 

​    @Cacheable(cacheNames = "dept",cacheManager = "deptCacheManager")

​    public Department getDeptById(Integer id){

​        System.out.println("查询部门"+id);

​        Department department = departmentMapper.getDeptById(id);

​        return department;

​    }

 

​    // 使用缓存管理器得到缓存，进行api调用

​    public Department getDeptById(Integer id){

​        System.out.println("查询部门"+id);

​        Department department = departmentMapper.getDeptById(id);

​        //获取某个缓存

​        Cache dept = deptCacheManager.getCache("dept");

​        dept.put("dept:1",department);

​        return department;

​    }

​    

​    //我自己认为是@Cacheable的代码实现

​    public Department getDeptById(Integer id){

​        System.out.println("查询部门"+id);

​        //获取某个缓存

​        Cache cache = deptCacheManager.getCache("dept");

​        Department department = cache.get("dept:" + id);

​        if(null == department){

​           department = departmentMapper.getDeptById(id);

​        }

​        return department;

​    }

}

 

！！！！！！！！！！！！！！！！！！！！！！！！！重要！！！！！！！！！！！！！！！！！！！！！！！！

@Cacheable是基于注解的方式，这个是原生的代码：不基于注解，使用缓存管理器得到缓存，进行api调用

Cache dept = deptCacheManager.getCache("dept");

dept.put("dept:1",department);

 

 

SpringBoot整合消息队列

Spring Boot自动配置：RabbitAutoConfiguration(引入了RabbitTemplate组件，给RabbitMq发送和接受消息；引入了AmqpAdmin组件，创建队列，交换器等)    

​                     ====>   RabbitProperties(prefix == spring.rabbitmq)

 

​    @Autowired

​    RabbitTemplate rabbitTemplate;

​    /**

​     \* 1、单播（点对点）

​     */

​    @Test

​    public void contextLoads() {

​        //object默认当成消息体，只需要传入要发送的对象，自动序列化发送给rabbitmq；

​        //rabbitTemplate.convertAndSend(exchage,routeKey,object);

​        Map<String,Object> map = new HashMap<>();

​        map.put("msg","这是第一个消息");

​        map.put("data", Arrays.asList("helloworld",123,true));

​        //对象被默认序列化以后发送出去

​        rabbitTemplate.convertAndSend("exchange.direct","atguigu.news",new Book("西游记","吴承恩"));   //发送消息时把路由键带上了

 

​    }

 

​    //接受数据,如何将数据自动的转为json发送出去

​    @Test

​    public void receive(){

​        Object o = rabbitTemplate.receiveAndConvert("atguigu.news");  //queueName

​        System.out.println(o.getClass());

​        System.out.println(o);

​    }

​    

​    序列化与反序列化机制：自定义一个Converter ：以json的形式转换数据

​    @Configuration

​    public class MyAMQPConfig {

​       @Bean

​       public MessageConverter messageConverter(){

​           return new Jackson2JsonMessageConverter();

​       }

​    }

 

单播与广播的区别在于：发送给的交换器类型不同，调用的方法都一样

​    

二：监听场景：

1.main方法上开启基于注解: @EnableRabbit (类似于@EnableCaching)

2.在服务类上:

  @RabbitListener(queues = [])

 

@Service

public class BookService {

​    @RabbitListener(queues = "atguigu.news")

​    public void receive(Book book){

​        System.out.println("收到消息："+book);

​    }

 

​    @RabbitListener(queues = "atguigu")

​    public void receive02(Message message){

​        System.out.println(message.getBody());

​        System.out.println(message.getMessageProperties());

​    }

}  

​    

三：程序中创建交换器、绑定规则、队列

AmqpAdmin

​    @Autowired

​    AmqpAdmin amqpAdmin;  //declare开头的是创建的意思

 

​    @Test

​    public void createExchange(){

 

​        amqpAdmin.declareExchange(new DirectExchange("amqpadmin.exchange"));    //创建哪种类型的Exchange，找到Exchange这个接口，ctrl+T，看他的实现类

​        amqpAdmin.declareQueue(new Queue("amqpadmin.queue",true));

​        //创建绑定规则

​        amqpAdmin.declareBinding(new Binding("amqpadmin.queue", Binding.DestinationType.QUEUE,"amqpadmin.exchange","amqp.haha",null));  //"amqp.haha"是路由键

​        //删除

​        //amqpAdmin.delete(xxxx);

​    }

 

介绍下：交换器、绑定规则、队列

消息有路由键，队列有绑定键

一个交换器可以绑定多个队列

消息发给消息代理这个服务器，服务器中有非常多的交换器和队列，交换器和消息队列绑定的，交换器接收到消息后，根据路由键判断交给哪个队列。

交换器有4种类型：

​    direct，fanout，topic，headers，headers几乎不用

​    direct：

​        消息中的路由键（routing key）如果和 Binding 中的 binding key 一致， 交换器就将消息发到对应的队列中。

​        路由键与队列名完全匹配，如果一个队列绑定到交换机要求路由键为“dog”，则只转发 routing key 标记为“dog”的消息，不会转发“dog.puppy”，

​        也不会转发“dog.guard”等等。它是完全匹配、单播的模式。

​    fanout:

​        每个发到 fanout 类型交换器的消息都会分到所有绑定的队列上去。fanout 交换器不处理路由键，只是简单的将队列绑定到交换器上，

​        每个发送到交换器的消息都会被转发到与该交换器绑定的所有队列上。很像子网广播，每台子网内的主机都获得了一份复制的消息。

​        fanout 类型转发消息是最快的。

​    topic：

​        topic 交换器通过模式匹配分配消息的路由键属性，将路由键和某个模式进行匹配，此时队列需要绑定到一个模式上。

​        它将路由键和绑定键的字符串切分成单词，这些单词之间用点隔开。

​        它同样也会识别两个通配符：符号“#”和符号“*”。#匹配0个或多个单词，*匹配一个单词。

 

============================================================Spring Boot整合Spring Data ElasticSearch    

Elasticsearch是一个分布式搜索服务，提供Restful API，底层基于Lucene，采用多shard（分片）的方式保证数据安全，并且提供自动resharding的功能    Elasticsearch。

内部使用 Lucene 做索引与搜索，但是它的目的是使全文检索变得简单， 通过隐藏 Lucene 的复杂性，取而代之的提供一套简单一致的 RESTful API。

Elasticsearch 是 面向文档 的，意味着它存储整个对象或 文档_。

Elasticsearch 不仅存储文档，而且 _索引 每个文档的内容使之可以被检索。在 Elasticsearch 中，你对文档进行索引、检索、排序和过滤--而不是对行列数据。    

Elasticsearch 使用 JSON 作为文档的序列化格式

存储数据到 Elasticsearch 的行为叫做 索引    

ES集群下有好多索引（类似Mysql的数据库），每个索引下有N个类型，（类似Mysql的表名），每个类型下都有多个文档（一个文档类似Mysql的一行表数据），文档是Json数组

例子：

每个雇员索引一个文档，包含该雇员的所有信息。

每个文档都将是 employee 类型 。

该类型位于 索引 megacorp 内。

该索引保存在我们的 Elasticsearch 集群中。直接发请求： [http://EsIp:9200//megacorp/employee/id](http://esip:9200/megacorp/employee/id)  PUT请求

PUT /megacorp/employee/1

{

​    "first_name" : "John",

​    "last_name" :  "Smith",

​    "interests": [ "sports", "music" ]

}

PUT /megacorp/employee/2

{

​    "first_name" : "John2",

​    "last_name" :  "Smith2",

​    "interests": [ "sports2", "music2" ]

}

注意，路径 /megacorp/employee/1 包含了三部分的信息：

megacorp：索引名称

employee：类型名称

1：特定雇员的ID

 

目前我们已经在 Elasticsearch 中存储了一些数据， 接下来就能专注于实现应用的业务需求了。第一个需求是可以检索到单个雇员的数据。

简单地执行 一个 HTTP GET 请求并指定文档的地址——索引库、类型和ID。 使用这三个信息可以返回原始的 JSON 文档：

GET /megacorp/employee/1

 

HEAD请求:返回 200 404，判断请求的数据有没有

Elasticsearch提供Restful API,和Restful url有点相似，但put是不同的，一个是更新，一个是新增

Elasticsearch的put：  第一次是添加create，第二次put同一个请求，但是请求的内容不一样，则是更新。

PUT /megacorp/employee/1                                ----------------------------create

{

​    "first_name" : "John",

​    "last_name" :  "Smith",

​    "interests": [ "sports", "music" ]

}

PUT /megacorp/employee/1                                ----------------------------update

{

​    "first_name" : "尼古拉斯-赵四",

​    "last_name" :  "Smith",

​    "interests": [ "sports", "music" ]

}

 

Restful url:

GET（SELECT）：从服务器取出资源（一项或多项）。

POST（CREATE）：在服务器新建一个资源。

PUT（UPDATE）：在服务器更新资源（客户端提供改变后的完整资源）。

PATCH（UPDATE）：在服务器更新资源（客户端提供改变的属性）。

DELETE（DELETE）：从服务器删除资源。

 

我们使用下列请求来搜索所有雇员：

GET /megacorp/employee/_search  回结果包括了所有三个文档，放在数组 hits 中

接下来，尝试下搜索姓氏为 ``Smith`` 的雇员：

GET /megacorp/employee/_search?q=last_name:Smith

 

Elasticsearch 提供一个丰富灵活的查询语言叫做 查询表达式 ， 它支持构建更加复杂和健壮的查询。

重写之前的查询所有 Smith 的搜索 ：这个请求使用 JSON 构造，一个 match 查询，属于查询类型之一

GET /megacorp/employee/_search

{

​    "query" : {

​        "match" : {

​            "last_name" : "Smith"

​        }

​    }

}

 

过滤器 filter ：

GET /megacorp/employee/_search

{

​    "query" : {

​        "bool": {

​            "must": {

​                "match" : {

​                    "last_name" : "smith"

​                }

​            },

​            "filter": {

​                "range" : {

​                    "age" : { "gt" : 30 }

​                }

​            }

​        }

​    }

}

 

全文搜索：

GET /megacorp/employee/_search

{

​    "query" : {

​        "match" : {

​            "about" : "rock climbing"

​        }

​    }

}

结果：

"hits": [

​         {

​            ...

​            "_score":         0.16273327,

​            "_source": {

​               "first_name":  "John",

​               "about":       "I love to go rock climbing"

​            }

​         },

​         {

​            ...

​            "_score":         0.016878016,

​            "_source": {

​               "first_name":  "Jane",

​               "about":       "I like to collect rock albums"

​            }

​         }

​      ]

Elasticsearch 默认按照相关性得分排序，Elasticsearch中的 相关性 概念非常重要，也是完全区别于传统关系型数据库的一个概念，数据库中的一条记录要么匹配要么不匹配。

GET /megacorp/employee/_search

{

​    "query" : {

​        "match_phrase" : {

​            "about" : "rock climbing"

​        }

​    }

}

精确匹配，结果只有一个

 

 

Elasticsearch的使用场景:

早期的搜索引擎不能提供耐用的存储或其他经常需要的功能，如统计。Elasticsearch是提供持久存储、统计等多项功能的现代搜索引擎。

Elasticsearch不支持包含频繁更新、事务（transaction）的操作。

 

ES作为存储的优势：

如果一台服务器出现故障时会发生什么？你可以通过复制 数据到不同的服务器以达到容错的目的。

ES不支持事务、复杂的关系（至少1.X版本不支持，2.X有改善，但支持的仍然不好），如果你的系统中需要上述特征的支持，需要考虑在原有架构、原有存储的基础上的新增ES的支持。相对安全的方式是：将ES作为新的组件添加到现有系统中。

 

为什么那么多工具适配Elasticsearch？主要原因如下：

1）Elasticsearch是开源的。

2）Elasticsearch提供了JAVA API接口。

3）Elasticsearch提供了RESTful API接口（不管程序用什么语言开发，任何程序都可以访问）

4）更重要的是，REST请求和应答是典型的JSON（JavaScript对象 符号）格式。通常情况下，一个REST请求包含一个JSON文件，其回复都 也是一个JSON文件。

 

Elasticsearch的功能

1.分布式的搜索引擎和数据分析引擎

2.全文检索，结构化检索，数据分析

3.对海量数据进行近实时的处理

 

 

elasticsearch聚合查询:

GET /tvs/sales/_search

{

  "size": 0,

  "aggs": {

​    "group_by_color": {

​      "terms": {

​        "field": "color"

​      },

​      "aggs": {

​        "avg_price": {

​          "avg": {

​            "field": "price"

​          }

​        },

​        "min_price" : {

​          "min": {

​            "field": "price"

​          }

​        },

​        "max_price" : {

​          "max": {

​            "field": "price"

​          }

​        },

​        "sum_price" : {

​          "sum": {

​            "field": "price"

​          }

​        }

​      }

​    }

  }

}

 

 

 

聚合搜索 设置 size:0 无效

curl -XPOST { "size" : 0, "aggs": { "group_by_state": { "terms": { "field": "brand_id" } } } } 结果还是只返回 10 行数据 ，sum_other_doc_count 不为 0

原因： 最外层的 size 是限制 hits 的，如果要设置 terms 聚合的桶数量， 要在 field 那一层设置 size

 

 

 

es 做聚合处理

将如下sql转换成es报文：

select

​    categoryname,

​    cmmdtyband,

​    cmmdtybanddec,

​    count (updatetime),

​    count (distinct extdrealpayamt),

​    sum (extdtotalamount)

from

​    lma_ases_magic_cube

where

​    createdate >= 20180729

and createdate <= 20180731

and categorycode in ('00001', '00002')

and categoryname = '冰洗'

group by

​    categoryname,

​    cmmdtyband,

​    cmmdtybanddec

​    

转换的es报文：

lma_ases_magic_cube/_search

{

​    "size": 0,

​    "query": {

​        "constant_score": {

​            "filter": {

​                "bool": {

​                    "must": [

​                        {

​                            "range": {

​                                "createdate": {

​                                    "gte": "20180729",

​                                    "lte": "20180731"

​                                }

​                            }

​                        },

​                        {

​                            "terms": {

​                                "categorycode": [

​                                    "00001",

​                                    "00002"

​                                ]

​                            }

​                        },

​                        {

​                            "term": {

​                                "categoryname": "冰洗"

​                            }

​                        

​                        }

​                    ]

​                }

​            }

​        }

​    },

​    "aggs": {

​        "terms_name": {

​            "terms": {

​                "script": {

​                    "inline": "doc['categoryname'].value + ';' + doc['cmmdtyband'].value + ';'+ doc['cmmdtybanddec'].value"

​                }

​            },

​            "aggs": {

​                "updatetime": {

​                    "value_count": {

​                        "field": "updatetime"

​                    }

​                },

​                "extdrealpayamt": {

​                    "cardinality": {

​                        "field": "extdrealpayamt"

​                    }

​                },

​                "extdtotalamount": {

​                    "sum": {

​                        "field": "extdtotalamount"

​                    }

​                }

​            }

​        }

​    }

}

 

你可能注意到了size:0，如果你只需要统计数据，不要数据本身，就设置它，这不是我投机取巧，官方文档也是这么干的。

 

 

 

percentiles 基于百分比统计

{

  "size": 0,

  "query": {

​    "filtered": {

​      "filter": {

​        "range": {

​          "@timestamp": {

​            "gt": "now-15m",

​            "lt": "now"

​          }

​        }

​      }

​    }

  },

  "aggs": {

​    "execute_time": {

​      "percentiles": {

​        "field": "upstream_time_ms",

​        "percents": [

​          90,

​          95,

​          99.9

​        ]

​      }

​    }

  }

}

 

//返回值，0.1%的请求超过了159ms

{

  "took": 620,

  "timed_out": false,

  "_shards": {

​    "total": 5,

​    "successful": 5,

​    "failed": 0

  },

  "hits": {

​    "total": 679400,

​    "max_score": 0,

​    "hits": []

  },

  "aggregations": {

​    "execute_time": {

​      "values": {

​        "90.0": 24.727003484320534,

​        "95.0": 72.6200981699678,

​        "99.9": 159.01065773524886 //99.9的数据落在159以内，是系统计算出来159

​      }

​    }

  }

}

 

percentile_ranks 指定一个范围，有多少数据落在这里

{

  "size": 0,

  "query": {

​    "filtered": {

​      "filter": {

​        "range": {

​          "@timestamp": {

​            "gt": "now-15m",

​            "lt": "now"

​          }

​        }

​      }

​    }

  },

  "aggs": {

​    "execute_time": {

​      "percentile_ranks": {

​        "field": "upstream_time_ms",

​        "values": [

​          50,

​          160

​        ]

​      }

​    }

  }

}

 

//返回值

 

{

  "took": 666,

  "timed_out": false,

  "_shards": {

​    "total": 5,

​    "successful": 5,

​    "failed": 0

  },

  "hits": {

​    "total": 681014,

​    "max_score": 0,

​    "hits": []

  },

  "aggregations": {

​    "execute_time": {

​      "values": {

​        "50.0": 94.14716385885366,

​        "160.0": 99.91130872493076 //99.9的数据落在了160以内，这次，160是我指定的，系统计算出99.9

​      }

​    }

  }

}

 

 

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

 

对某个字段进行聚合统计:

curl -X GET "[elasticsearch.in.netwa.cn:9200/my_index/_search](http://elasticsearch.in.netwa.cn:9200/my_index/_search)" -H 'Content-Type: application/json' -d'

{

  "aggs": {

​    "all_interests": {

​      "terms": { "field": "first_tag" }

​    }

  }

}

结果如下：

{"took":1,"timed_out":false,"_shards":{"total":5,"successful":5,"skipped":0,"failed":0},

"hits":{"total":123,"max_score":1.0,"hits":[...]},

"aggregations":{

"all_interests":

{"doc_count_error_upper_bound":0,

"sum_other_doc_count":1,

"buckets":[

{"key":"自然","doc_count":36},

{"key":"地理","doc_count":32},

{"key":"人文","doc_count":55}]

}}}

hits中的total显示了所有统计的文档数量：123

aggregations展示了聚合统计的结果

buckets包含了多个统计结果，first_tag字段统计的结果分别是：

自然：36

地理：32

人文：55

 

 

将查询结果在进行聚合统计:

curl -X GET "[elasticsearch.in.netwa.cn:9200/my_index/_search](http://elasticsearch.in.netwa.cn:9200/my_index/_search)" -H 'Content-Type: application/json' -d'

{

  "query": {

​        "term": {

​            "first_tag": "自然"

​        }

​    },

  "aggs": {

​    "all_interests": {

​      "terms": { "field": "second_tag" }

​    }

  }

}

结果如下：

 

{"took":1,"timed_out":false,"_shards":{"total":5,"successful":5,"skipped":0,"failed":0},"hits":{"total":36,"max_score":2.2581334,"hits":[...]},"aggregations":{"all_interests":{"doc_count_error_upper_bound":0,"sum_other_doc_count":0,"buckets":[{"key":"生物","doc_count":12},{"key":"常识","doc_count":10},{"key":"天文","doc_count":14}]}}}

hits中的total显示了所有统计的文档数量36

buckets包含了多个统计结果，first_tag字段统计的结果分别是：

生物：12

常识：10

天文：14

 

对多个字段同时进行聚合统计:

curl -X GET "[elasticsearch.in.netwa.cn:9200/my_index/_search](http://elasticsearch.in.netwa.cn:9200/my_index/_search)" -H 'Content-Type: application/json' -d'

{

  "aggs": {

​    "all_interests": {

​      "terms": { "field": "first_tag" },

​      "aggs": {

​        "all_interests": {

​            "terms": { "field": "second_tag" }

​        }

​      }

​    }

  }

}

结果如下：

{"took":3,"timed_out":false,"_shards":{"total":5,"successful":5,"skipped":0,"failed":0},"hits":{"total":123,"max_score":1.0,"hits":[...]},"aggregations":{"all_interests":{"doc_count_error_upper_bound":0,"sum_other_doc_count":1,"buckets":[{"key":"人文","doc_count":55,"all_interests":{"doc_count_error_upper_bound":0,"sum_other_doc_count":0,"buckets":[{"key":"文学","doc_count":20},{"key":"艺术","doc_count":35}]}},{"key":"自然","doc_count":36,"all_interests":{"doc_count_error_upper_bound":0,"sum_other_doc_count":0,"buckets":[{"key":"生物","doc_count":12},{"key":"常识","doc_count":10},{"key":"天文","doc_count":14}]}},{"key":"地理","doc_count":32,"all_interests":{"doc_count_error_upper_bound":0,"sum_other_doc_count":0,"buckets":[{"key":"人文地理","doc_count":11},{"key":"自然地理","doc_count":21}]}}]}}}

 

hits中的total显示了所有统计的文档数量123

buckets包含了多个统计结果，first_tag及包含的second_tag字段统计的结果分别是：

人文：55，{文学：20，艺术：35}

自然：36 ，{生物：12，常识：10，天文：14}

地理：32 ，{人文地理：11，自然地理：21}

 

===============================================================================Servlet的生命周期===================================================

1.创建Servlet对象，通过服务器反射机制创建Servlet对象，第一次请求时才会创建。（默认）

 

2，调用Servlet对象的init()方法，初始化Servlet的信息，init()方法只会在创建后被调用一次；

 

3，响应请求，调用service()或者是doGet()，doPost()方法来处理请求，这些方法是运行的在多线程状态下的。

 

4，在长时间没有被调用或者是服务器关闭时，会调用destroy()方法来销毁Servlet对象。    

 

Servlet的生命周期从Servlet类加载，到创建Servlet类实例，Servlet的初始化（init()  真正成为一个Servlet），

有请求到来，调用service方法（主要工作），直到Servlet被destroy；

 

1.Servlet类加载：

1.1  启动web容器后，容器去寻找应用的部署描述文件（web.xml），从部署描述文件中读取到上下文初始化参数，此时创建一个ServletContext对象，应用的所有部分共享此上下文；

1.2  容器为context-param创建String名值对（参数名和参数值均为String类型）；

1.3  容器将名值对交给ServletContext对象；

1.4  如果在部署描述文件中有Listener标签的话，创建Listener实例；

1.5  容器调用Listener的contextInitialized方法，传入ServletContextEvent对象，此对象包含一个ServletContext引用，事件处理代码可以得到上下文初始化参数。

 

2.创建Servlet类实例：

2.1  容器读取部署描述文件中的Servlet标签，包括初始化参数（init-param）；

2.2  容器创建ServletConfig实例；！！！！！！！！！！！！！！！执行构造器方法，只在第一次时执行，这说明servlet是单例的，有线程安全问题

2.3  容器为servlet初始化参数创建名值对；

2.4  容器用名值对填充ServletConfig；

2.5  容器创建Servlet类的新实例（一般在第一次请求到来时创建，也可通过设置load-on-start参数在容器启动时创建）。

 

3.Servlet初始化：

Servlet的init方法在一个生命周期中只被执行一次，调用service方法前，初始化必须完成；

在GenericServlet中有两个init方法，其中有参数的init方法，调用了无参的init方法，所以，若需要重写init方法，只需要重写无参的。

 

4.Servlet的service方法：

每次请求到来，都会调用service方法，在HttpServlet中，service方法用于判断请求的方法（不用重写），而去重写doGet方法或doPost方法。

 

5.Servlet的destroy方法：

销毁Servlet实例时调用，意味着Servlet的生命周期结束。

 

 

复习Servlet：

是一个java类，只不过他是部署运行在servlet容器（tomcat）中，所以其要映射到web.xml中

servlet容器：掌控servlet的生命周期：可以来创建servlet，并调用servlet相关生命周期方法。还有filter、listener

servlet是一个接口，是运行在服务器端的Java组件，在web.xml中配置它

init()  和 构造器方法 有一点不同之处：  init(ServletConfig config)

Servlet的生命周期的方法都是由tomcat调用的。

在web.xml中配置 servlet时，有一个属性 load-on-startup 如果写为1，表示tomcat启动时就创建这个servlet，默认是由请求到servler

load-on-startup 的值表示 启动的顺序，有好几个servlet时，值越小 越先执行。

 

一个Servlet可以有多个Servlet-Mapping，url-pattern 格式固定： 1.   以/开头并以/*结尾。  2.   *.拓展名

 

ServletConfig封装了Servlet的配置信息，并且可以获取ServletContext对象。了解：可以获取servlet的初始化参数（web.xml中配置Servlet的init-param）

ServletConfig是一个接口，也是tomcat实现的

 

ServletContext：Servlet的上下文，一个web应用的所有Servlet共用一个servlet，也叫application对象。ServletConfig.getServletContext()

web.xml中：全局配置

<context-param>

   <param-name>

   <param-value>

</context-param>

 

1.ServletContext可以获取当前web应用的初始化参数。ServletContext.getInitParameter(String name)

2.ServletContext可以获取当前web应用某一个文件在服务器上的绝对路径，而不是部署之前的物理路径(文件右键peoperties)。ServletContext.getRealPath(String filePath)  例：ServletContext.getRealPath("/note.txt")  /代表web应用跟目录

3.ServletContext可以获取当前web应用的名称： ServletContext.getContextPath()  /day_29

4.ServletContext可以获取当前web应用某一个文件的输入流。ServletContext.getResourceAsStream(String filePath)  filePath:当前web应用的path,即服务器上的路径

   src目录下，新建a.properties

   InputStream in = getClass().getClassLoader().getResourceAsStream("a.properties");

   InputStream in = ServletContext.getRealPath("/WEB-INF/classes/a.properties");   /当前web应用的跟目录

 

servlet的service(ServletRequest request,ServletResponse response)

HttpServletRequest是ServletRequest的子接口。针对于Http请求定义

HttpServletRequest re = (HttpServletRequest)request

re.getRequestURI():  /day_29/login

re.getMethod():  GET/POST

re.getQueryString(): ?后的字符串，POST的话为null

re.getServletPath(): /login

 

HttpServletResponse 中有个 sendRedirect()

 

http://127.0.0.1:8080/cmd_helloworld/?name=guowuxin

此时URI uri = exchange.getRequestURI（）；

通过uri可以拿到连接的各部分内容：

uri.getPath（） --------------------> /cmd_helloworld 注意有斜杠

uri.getQuery（）----------------------> name=guowuxin

 

 

HttpServlet继承了GenericServlet，而GenericServlet实现Servlet接口

HttpServlet

​        \- HttpServlet继承了GenericServlet，而GenericServlet实现Servlet接口

​        \- 所以我们可以同构继承HttpServlet来创建一个Servlet。

​        \- HttpServlet重写service()方法：

​            1.在该方法中先将ServletRequest和ServletResponse

​                强转为了HttpServletRequest和HttpServletResponse。

​            2.然调用重载的service()方法，并将刚刚强转得到对象传递到重载的方法中。

​        \- 重载service(HttpServletRequest request , HttpServletResponse response)

​            1.在方法中获取请求的方式（get或post）

​            2.在根据不同的请求方式去调用不同的方法：

​                如果是GET请求，则调用doGet(HttpServletRequest request , HttpServletResponse response)

​                如果是post请求，则调用doPost(HttpServletRequest request , HttpServletResponse response)

​        \- 结论：

​            当通过继承HttpServlet来创建一个Servlet时，我们只需要根据要处理的请求的类型，来重写不同的方法。

​                处理get请求，则重写doGet()

​                处理post请求，则重写doPost()

===============================================================================消息中间件==========================================================

大多应用中，可通过消息服务中间件来提升系统异步通信、扩展解耦能力

 

消息服务中两个重要概念：

​    消息代理（message broker）和目的地（destination）

​    消息代理：消息中间件的服务器，要往消息队列中存内容，就要先连接消息中间件的服务器，消息发送者将消息发送给消息代理，消息代理接管消息后，再将消息发送到一个目的地。

当消息发送者发送消息以后，将由消息代理接管，消息代理保证消息传递到指定目的地。

两种形式的目的地

队列（queue）：点对点消息通信（point-to-point）：

​               消息发送者发送消息，消息代理将其放入一个队列中，多个消息接收者自己从队列中获取消息内容，消息读取后被移出队列，不会被其他消息接收者再拿到

主题（topic）：发布（publish）/订阅（subscribe）消息通信：

​               发送者（发布者）发送消息到主题，多个接收者（订阅者）监听（订阅）这个主题，那么就会在消息到达时同时收到消息

 

以用户注册的场景来讨论此问题：

通常情况下：

用户注册 ======》 注册信息写入数据库  ======》发送注册邮件  ======》发送注册短信， 此时用户收到消息注册成功

消息队列：

用户注册 ======》 注册信息写入数据库  ======》注册信息写入消息队列，此时用户收到消息注册成功  <------------------发送注册邮件 异步读取消息队列

​                                                        /|\

​                                                         |  

​                                                         |----------------------------发送注册短信 异步读取消息队列

2.系统解耦：(2个系统：微服务)

通常情况下：

订单系统------------------------------->库存系统                                                        

​               调用库存系统接口                                                        

现在：

订单系统------------------------------->消息队列<-------------------------------库存系统                                                    

​                    写入                                       订阅            

​                    

3.流量削峰，秒杀：

用户请求------------->消息队列，定长500<-------------tomcat秒杀业务处理，而不是成千上万个请求一起来请求tomcat

 

AMQP（Advanced Message Queuing Protocol）

高级消息队列协议，也是一个消息代理的规范，兼容JMS，RabbitMQ是AMQP的实现

AMQP定义了wire-level层的协议标准；天然具有跨平台、跨语言特性。

支持消息类型：byte[]，当实际应用时，有复杂的消息，可以将消息序列化后发送。

Spring Boot自动配置：RabbitAutoConfiguration    

RabbitMQ：    

   Message：消息，消息是不具名的，它由消息头和消息体组成。消息体是不透明的，而消息头则由一系列的可选属性组成，

​            这些属性包括routing-key（路由键）、priority（相对于其他消息的优先权）、delivery-mode（指出该消息可能需要持久性存储）等。

   Publisher：消息的生产者，也是一个向交换器发布消息的客户端应用程序。                                        

   Exchange： 交换器，用来接收生产者发送的消息并将这些消息路由给服务器中的队列。

​              Exchange有4种类型：direct(默认)，fanout, topic, 和headers，不同类型的Exchange转发消息的策略有所区别

​              交换器就已经在消息代理里面了。是里面一个组件，上面绑定了很多的队列，通过路由键，来指定具体放到哪个队列里。

   Channel：如果每次从消息队列中取一条消息都建立一个TCP连接，那么这会非常的消耗性能  =====》  只建立一个tcp连接，在一个tcp中开多个信道。                                                

 

===============================================================================单例模式强化==========================================================

双端检索机制：

public class C{

​    private C(){}

​    private static volatile A a = null;

​    public static A getInstance(){

​        if(null == a){    

​            synchronized(A.class){

​               if(null == a){

​                   a = new A();

​               }

​            }

​         }

​         return a;

​    }

}

 

 

===============================================================================Spring注入==========================================================

<bean id="autotest" class="autotest" autowire="constructor">  

</bean>

​         

<!-- 当 Spring 容器启动时，AutowiredAnnotationBeanPostProcessor 将扫描 Spring 容器中所有 Bean，当发现 Bean 中拥有 @Autowired 注释时就找到和其匹配(默认按类型匹配)的 Bean，并注入到对应的地方中去-->

<bean class="org.springframework.beans.factory.annotation.AutowiredAnnotationBeanPostProcessor"/>

​        

<bean id="person" class="Person">  

   <property name="age" value="21"></property>  

   <property name="name" value="李跃"></property>  

   <property name="sex" value="男"></property>  

</bean>

 

 

public class autotest {      

​    @Autowired//这里用了这个注释就省去了构造方法或者get，set方法来设置person属性  

​    private Person person;

}   

  

 

或者：  eSight用的这种方法

<bean id="autotest" class="Autotest" >  

​    <property name="person" ref="person"></property>  

</bean>

​         

<bean id="person" class="Person">  

​    <property name="age" value="21"></property>  

​    <property name="name" value="李跃"></property>  

​    <property name="sex" value="男"></property>  

</bean>  

 

 

public class Autotest {  

​    private Person person;

​    public Person getPerson() {

​        return person;

​    }

​    public void setPerson(Person person) {

​        this.person = person;

​    }

​    

​    ConfigurableApplicationContext cf=new ClassPathXmlApplicationContext("spring-mvc.xml");      

​    Autotest autotest=(Autotest)cf.getBean("autotest");  

}

 

 

或者：

<bean id="autotest" class="autotest"/>  

​          

<!-- 当 Spring 容器启动时，AutowiredAnnotationBeanPostProcessor 将扫描 Spring 容器中所有 Bean，当发现 Bean 中拥有 @Autowired 注释时就找到和其匹配(默认按类型匹配)的 Bean，并注入到对应的地方中去-->

<bean class="org.springframework.beans.factory.annotation.AutowiredAnnotationBeanPostProcessor"/>

​         

<bean id="person" class="Person">  

​    <property name="age" value="21"></property>  

​    <property name="name" value="李跃"></property>  

​    <property name="sex" value="男"></property>  

</bean>  

 

 

public class autotest{

​    private Person person;

​    

​    public void fun(){  

​           ConfigurableApplicationContext cf=new ClassPathXmlApplicationContext("spring-mvc.xml");      

​           autotest autotest=(autotest)cf.getBean("autotest");   

​          

​           System.out.println(autotest.person); //Person@4f970963

​           System.out.println(this); //autotest@2f92e0f4

​           System.out.println(autotest); //autotest@7b49cea0

​           System.out.println(this.person);//null,   

​    }  

​       

​    public Person getPerson() {

​        System.out.println(person);

​        return person;

​    }

​    

​    @Autowired

​    public void setPerson(Person person) {

​        this.person = person;

​    }

​    public static void main(String args[]){  

​           new autotest().fun(); // (new autotest()==B)调用A==b.a.fun()

​    }  

}  

 

 

@Configuration

@EnableWebSecurity

public class SecurityConfig extends WebSecurityConfigurerAdapter {

 

​    @Autowired

​    public void configureGlobal(AuthenticationManagerBuilder auth) throws Exception {

​        auth

​            .inMemoryAuthentication()

​                .withUser("user").password("password").roles("USER");

​    }

}

这段代码里，是不是auth是被注入的？configureGlobal被调用的时机又是什么时候？

Spring会先实例化所有Bean，然后根据配置进行扫描，当检测到@Autowired后进行注入auth，注入时调用configureGlobal这个方法。

 

===============================================================================Mybatis like==========================================================

name LIKE '%#{name}%'     此方法错误 ：      (‘%#{name}%’)会变为(‘%?%’)

解决办法：

把’%#{name}%’改为”%”#{name}”%”         ：    AND name LIKE "%"#{name}"%"

   <select id="searchStudents" resultType="com.example.entity.StudentEntity"

​        parameterType="com.example.entity.StudentEntity">

​        SELECT * FROM test_student

​        <where>

​            <if test="age != null and age != '' and compare != null and compare != ''">

​                age

​                ${compare}

​                \#{age}

​            </if>

​            <if test="name != null and name != ''">

​                AND name LIKE "%"#{name}"%"

​            </if>

​            <if test="address != null and address != ''">

​                AND address LIKE "%"#{address}"%"

​            </if>

​        </where>

​        ORDER BY id

​    </select>

使用sql中的字符串拼接函数              ：    AND name LIKE CONCAT(CONCAT('%',#{name},'%'))

 

使用标签：

  <select id="searchStudents" resultType="com.example.entity.StudentEntity"

​        parameterType="com.example.entity.StudentEntity">

​        <bind name="pattern1" value="'%' + _parameter.name + '%'" />

​        <bind name="pattern2" value="'%' + _parameter.address + '%'" />

​        SELECT * FROM test_student

​        <where>

​            <if test="age != null and age != '' and compare != null and compare != ''">

​                age

​                ${compare}

​                \#{age}

​            </if>

​            <if test="name != null and name != ''">

​                AND name LIKE #{pattern1}

​            </if>

​            <if test="address != null and address != ''">

​                AND address LIKE #{pattern2}

​            </if>

​        </where>

​        ORDER BY id

​    </select>

 

Mybatis中的 ${} 和 #{}区别与用法：

​     \#{}方式能够很大程度防止sql注入。

​     $方式无法防止Sql注入。

​     $方式一般用于传入数据库对象，例如传入表名.

​     一般能用#的就别用$.

例如：select * from ${prefix}ACT_HI_PROCINST where PROC_INST_ID_ = #{processInstanceId}    

  

===============================================================================Map  Null==========================================================

HashTable :  key/value 都不能为null ，线程安全

ConcurrentHashMap ： key/value 都不能为null ，线程局部安全

TreeMap ： key不能为null，value可以为null ，线程不安全

HashMap ： key/value 都可以为null ，线程不安全

LinkedHashMap : key/value 都可以为null ，线程不安全

 

迭代HashMap的顺序并不是HashMap放置的顺序，也就是无序。HashMap的这一缺点往往会带来困扰，因为有些场景，我们期待一个有序的Map。

这个时候，LinkedHashMap就闪亮登场了

 

 

===============================================================================LinkedHashMap==========================================================

利用LinkedHashMap实现LRU算法缓存

 

LRU即Least Recently Used，最近最少使用，也就是说，当缓存满了，会优先淘汰那些最近最不常访问的数据。比方说数据a，1天前访问了；数据b，2天前访问了，缓存满了，优先会淘汰数据b。

LinkedHashMap提供了一个boolean值可以让用户指定是否实现LRU

 

public LinkedHashMap(int initialCapacity,

​         float loadFactor,

​                     boolean accessOrder) {

​    super(initialCapacity, loadFactor);

​    this.accessOrder = accessOrder;

}

 

就是这个accessOrder，它表示：

（1）false，所有的Entry按照插入的顺序排列

（2）true，所有的Entry按照访问的顺序排列

 

第二点的意思就是，如果有1 2 3这3个Entry，那么访问了1，就把1移到尾部去，即2 3 1。 每次访问都把访问的那个数据移到双向队列的尾部去，那么每次要淘汰数据的时候，双向队列最头的那个数据不就是最不常访问的那个数据了吗？换句话说，双向链表最头的那个数据就是要淘汰的数据。

 

“访问”，这个词有两层意思：

1、根据Key拿到Value，也就是get方法

2、修改Key对应的Value，也就是put方法

 

 

代码演示LinkedHashMap按照访问顺序排序的效果：

public static void main(String[] args)

{

​    LinkedHashMap<String, String> linkedHashMap =

​            new LinkedHashMap<String, String>(16, 0.75f, true);

​    linkedHashMap.put("111", "111");

​    linkedHashMap.put("222", "222");

​    linkedHashMap.put("333", "333");

​    linkedHashMap.put("444", "444");

​    loopLinkedHashMap(linkedHashMap);

​    linkedHashMap.get("111");

​    loopLinkedHashMap(linkedHashMap);

​    linkedHashMap.put("222", "2222");

​    loopLinkedHashMap(linkedHashMap);

}

​     

public static void loopLinkedHashMap(LinkedHashMap<String, String> linkedHashMap)

{

​    Set<Map.Entry<String, String>> set = inkedHashMap.entrySet();

​    Iterator<Map.Entry<String, String>> iterator = set.iterator();

​     

​    while (iterator.hasNext())

​    {

​        System.out.print(iterator.next() + "\t");

​    }

​    System.out.println();

}

 

代码运行结果：

111=111    222=222    333=333    444=444   

222=222    333=333    444=444    111=111   

333=333    444=444    111=111    222=2222

 

代码运行结果证明了两点：

1、LinkedList是有序的；

2、每次访问一个元素（get或put），被访问的元素都被提到最后面去了。

 

===============================================================================ConcurrentHashMap的线程安全问题=======================================================================

public class BookTest {

​    private static final ConcurrentMap<String, AtomicInteger> CACHE_MAP = new ConcurrentHashMap<String, AtomicInteger>();

​    private static final String KEY = "test";

 

​    private static class TestThread implements Runnable{

​        @Override

​        public void run() {

​            if(CACHE_MAP.get(KEY)==null){

​                try {

​                    Thread.sleep(2000);

​                } catch (InterruptedException e) {

​                    e.printStackTrace();

​                }

​                CACHE_MAP.put(KEY, new AtomicInteger());

​            }

​            CACHE_MAP.get(KEY).incrementAndGet();

​        }

​    }

​    

​    public static void main(String[] args) {

​        new Thread(new TestThread()).start();

​        new Thread(new TestThread()).start();

​        new Thread(new TestThread()).start();

​        try {

​            Thread.sleep(2000);

​        } catch (InterruptedException e) {

​            e.printStackTrace();

​        }

​        System.out.println("次数:"+CACHE_MAP.get(KEY).get());    

​    }

}

结果：

次数:1

 

我们有3个线程取访问，照理来说应该是3才对，为什么是1呢？

其实ConcurrentHashMap的put方法跟普通的HashMap没什么区别，如果key相同，依然会覆盖。

要想达到不覆盖，我们可以使用putIfAbsent()方法。

将CACHE_MAP.put(KEY, new AtomicInteger());

改为CACHE_MAP.putIfAbsent(KEY, new AtomicInteger());

结果：

次数:3

 

 

 

http://www.importnew.com/29832.html

 

 

我们上述所讲的Map(HashMap、LinkedHashMap)都是非线程安全的，这意味着不应该在多个线程中对这些Map进行修改操作，轻则会产生数据不一致的问题，

甚至还会因为并发插入元素而导致链表成环（插入会触发扩容，而扩容操作需要将原数组中的元素rehash到新数组，这时并发操作就有可能产生链表的循环引用从而成环），

这样在查找时就会发生死循环，影响到整个应用程序。

Collections.synchronizedMap(Map<K,V>m)可以将一个Map转换成线程安全的实现，其实也就是通过一个包装类，然后把所有功能都委托给传入的Map实现，

而且包装类是基于synchronized关键字来保证线程安全的（时代的眼泪Hashtable也是基于synchronized关键字），

底层使用的是互斥锁（同一时间内只能由持有锁的线程访问，其他竞争线程进入睡眠状态），性能与吞吐量差强人意。

 

ConcurrentHashMap没有使用一个全局锁来锁住自己，而是采用了减少锁粒度的方法，尽量减少因为竞争锁而导致的阻塞与冲突，而且ConcurrentHashMap的检索操作是不需要锁的。

在Java 7中，ConcurrentHashMap把内部细分成了若干个小的HashMap，称之为段（Segment），默认被分为16个段。对于一个写操作而言，会先根据hash code进行寻址，得出该Entry应被存放在哪一个Segment，然后只要对该Segment加锁即可。理想情况下，一个默认的ConcurrentHashMap可以同时接受16个线程进行写操作（如果都是对不同Segment进行操作的话）

分段锁对于size()这样的全局操作来说就没有任何作用了，想要得出Entry的数量就需要遍历所有Segment，获得所有的锁，然后再统计总数。事实上，ConcurrentHashMap会先试图使用无锁的方式统计总数，这个尝试会进行3次，如果在相邻的2次计算中获得的Segment的modCount次数一致，代表这两次计算过程中都没有发生过修改操作，那么就可以当做最终结果返回，否则，就要获得所有Segment的锁，重新计算size。

 

Java8的ConcurrentHashMap，它与Java7的实现差别较大。完全放弃了段的设计，而是变回与HashMap相似的设计，

使用buckets数组与分离链接法（同样会在超过阈值时树化，对于构造红黑树的逻辑与HashMap差别不大，只不过需要额外使用CAS来保证线程安全）锁的粒度也被细分到每个数组元素（个人认为这样做的原因是因为HashMap在Java 8中也实现了不少优化，即使碰撞严重，也能保证一定的性能，而且Segment不仅臃肿还有弱一致性的问题存在），所以它的并发级别与数组长度相关（Java 7则是与段数相关）。

 

 

 

===============================================================================map的put和putIfAbsent使用======================================================================

来深入理解一下他们两个之间的区别，首先我们知道Map底层的实现是通过二叉树来实现的，这样一来我们就会在脑子里面呈现出二叉树的样子，给大家来个简单的：

 

public class Main {

​    public static void main(String[] args) {

​        ConcurrentMap<String, String> map = new ConcurrentHashMap<>();

​        map.put("1", "1");

 

​        System.out.println(map.putIfAbsent("1", "2"));

​        System.out.println(map.get("1"));

​        System.out.println(map.put("1", "3"));

​        System.out.println(map.get("1"));

​    }

}

结果：

1

1

1

3

 

ConcurrentMap<String, String> map = new ConcurrentHashMap<String, String>();

map.put("1", "1");

System.out.println(map.putIfAbsent("2", "2"));

System.out.println(map.get("2"));

结果：

null

2

 

我们如果用put保存数据的时候，map会检查当前树种是否有相同的key，如果有就替换，没有就保存，而putIfAbsent() 方法则不会，如果map中存在当前相同的键值，那么就把value赋值给当前的value，如果没有就进行存储

putIfAbsent() ： 如果指定的键未与某个值关联（或映射到null），则将其与给定值关联并返回null，否则返回当前值。

如果要实现并发，则必须重写该方法，这样的话，其用法就很明白了。

 

ConcurrentMap能够保证每一次调用（例如一次putIfAbsent）都是原子操作，不受多线程影响，但并不保证多次调用之间也是原子操作。

 

public class ChmTest2 {

​    public static void main(String[] args) {

​        final ConcurrentHashMap<Integer, String> chm = new ConcurrentHashMap<Integer, String>();

​        ExecutorService newFixedThreadPool = Executors.newFixedThreadPool(10);

​        newFixedThreadPool.submit(new Runnable() {

​            public void run() {

​                for(int i = 0;i <1000000;i++){

​                    chm.put(123, "asd"+i);

​                }

​            }

​        });

​        newFixedThreadPool.submit(new Runnable() {

​            public void run() {

​                System.out.println(chm.get(123));

​            }

​        });

​        newFixedThreadPool.shutdown();

​    }

}

通过多次运行发现，每次get的值都是不一样的，但如果保证get值一样的，那么就考虑串行了。

 

===============================================================================Volatile======================================================================

！！！！！！！！！！！！！！！！！！！！！！！！！ JVM为每一个线程，分配一个独立的缓存，用于提高效率。！！！！！！！！！！！！！！！！！！！！

内存可见性的问题：

​     JVM为每一个线程，分配一个独立的缓存，用于提高效率。

​     2个线程在操作一个共享数据时，对共享数据的操作，彼此不可见

 

例子：

​     public class A{

​          main(){

​               B b = new B();

​               new Thread(b).start();

​               while(true){

​                   if(b.isFlag()){

​                      sysout('main Thread flag ：' + b.isFlag());

​                      break;

​                   }

​               }

​          }

​     }

​     class B implements Runnable{    

​          private boolean flag = false;    //因为是内部类，所以是共享变量

​          public isFlag(){

​              return flag;

​          }

​          @Override

​          public void run(){

​               Thread.sleep(2000);

​               flag = true;

​               sysout('sub Thread flag ：' + isFlag());

​          }

​     }

 

​     结果：

​     sub Thread flag ：true

​     main Thread flag ：直接没打印，说明其是false；

 

2个线程在操作一个共享数据时，对共享数据的操作，彼此不可见，此时怎么解决呢？

可以加同步锁 ： synchronized

加锁，每次获得锁，会刷新缓存

​     public class A{

​          main(){

​               B b = new B();

​               new Thread(b).start();

​               while(true){

​                   synchronized(b){                //我去，B居然不要加锁

​                      if(b.isFlag()){

​                         sysout('main Thread flag ：' + b.isFlag());

​                         break;

​                      }

​                   }

​               }

​          }

​     }

加锁，在多线程下产生效率问题====》

volatile： 多个线程在操作共享数据时，可以保证内存中的数据是可见的。可以理解操作都是在主存中完成的

​     class B implements Runnable{    

​          private volatile boolean flag = false;

​     }

小总节：

多线程操作共享数据：   加锁、volatile

volatile相较于synchronized 是一个轻量级的同步策略

区别： synchronized 是互斥锁，volatile不具有互斥性，多个线程可以同时访问共享变量。

​       volatile不能保证变量的原子性

 

===============================================================================atomic==========================================================

AtomicInteger  ：  volatile (内存可见性)  +  CAS算法(原子性)   CAS算法 比 锁效率高

AtomicIntegerArray ： 数组中的每一个元素都是原子性的

 

CAS算法可以理解是无锁的同步机制

===============================================================================ConcurrentHashMap==========================================================

Collections.synchronizedMap(HashMap map)  这个方法就是给Map的各个方法的加上synchronized

 

jdk1.7  和 jdk1.8 的ConcurrentHashMap 完全不一样的实现。

ConcurrentHashMap ： 锁分段机制

16个段，每个段都是独立的锁，独立的表   也就可以支持16个线程同时访问

ConcurrentHashMap 底层也是CAS

 

ConcurrentSkipListMap 优于同步的 TreeMap

多线程访问一个给定的Collection时， ConcurrentHashMap 优于同步的 HashMap

 

当期望的读数和遍历远远大于列表的更新数时，CopyOnWriteArrayList 优于同步的 ArrayList。  CopyOnWriteArrayList添加操作不能太多，每次添加都会复制一下。适合并发迭代。

 

CopyOnWriteArrayList：  写入并复制

 

​     public class A{

​          main(){

​               B b = new B();

​               int i = 0;

​               while(i < 10){

​                   new Thread(b).start();

​                   i++;

​               }

​          }

​     }

​     class B implements Runnable{    

​          private static List<String> list = Collections.synchronizedList(new ArrayList<String>());

​          static{

​              list.add('AA');

​              list.add('BB');

​              list.add('CC');

​          }

​          @Override

​          public void run(){

​              Iterator<String>  it = list.iterator();   //但其iterator()操作还不是线程安全的。

​              while(it.hasNext()){

​                  sysout(it.next());

​                  list.add('AA');

​              }

​          }

​     }

​    

10个线程来并发的执行：

​      Iterator<String>  it = list.iterator();

​      while(it.hasNext()){

​         sysout(it.next());

​         list.add('AA');

​      }    

结果： 直接抛异常，并发修改异常 ConcurrentModificationException    

​    

如果把 private static List<String> list = Collections.synchronizedList(new ArrayList<String>());

换成   private static CopyOnWriteArrayList<String> list = new CopyOnWriteArrayList<String>();

​       每次 list.add('AA'); 底层都会完成1次复制，复制一个新的列表，再添加。  这里的write是加的意思。

​    

​    

​    

ConcurrentHashMap 的 局部线程安全问题：

虽然ConcurrentHashMap是线程安全的，但是如果你操作的是其本身，并如果使用不当，也会造成很多线程安全问题

public class ConcurrentHashMapTest {

​    private static final ConcurrentMap<String, AtomicInteger> CACHE_MAP = new ConcurrentHashMap<>();

​    private static final String KEY = "test";

 

​    private static class TestThread implements Runnable{

​        @Override

​        public void run() {

​            if(CACHE_MAP.get(KEY)==null){

​                try {

​                    Thread.sleep(200);

​                } catch (InterruptedException e) {

​                    e.printStackTrace();

​                }

​                CACHE_MAP.put(KEY, new AtomicInteger());

​            }

​            CACHE_MAP.get(KEY).incrementAndGet();

​        }

​    }

 

​    public static void main(String[] args) {

​        new Thread(new TestThread()).start();

​        new Thread(new TestThread()).start();

​        new Thread(new TestThread()).start();

​        try {

​            Thread.sleep(800);

​        } catch (InterruptedException e) {

​            e.printStackTrace();

​        }

​        System.out.println("次数:"+CACHE_MAP.get(KEY).get());

​    }

}    

运行结果：

次数:1    

​    

我们有3个线程取访问，照理来说应该是3才对，为什么是1呢？

其实ConcurrentHashMap的put方法跟普通的HashMap没什么区别，如果key相同，依然会覆盖。

要想达到不覆盖，我们可以使用putIfAbsent()方法。

将CACHE_MAP.put(KEY, new AtomicInteger());

改为CACHE_MAP.putIfAbsent(KEY, new AtomicInteger());    

​    

运行结果如下：

次数:3    

​    

在JDK1.7中，ConcurrentHashMap的数据结构是由一个Segment数组和多个HashEntry组成的    

JDK1.8的实现已经摒弃了Segment的概念，而是直接用Node数组+链表+红黑树的数据结构来实现    

​    

HashMap为什么线程不安全：

主要是两方面,首先如果多个线程同时使用put方法添加元素，而且假设正好存在两个put的key发生了碰撞(hash值一样)，那么根据HashMap的实现，

这两个key会添加到数组的同一个位置，这样最终就会发生其中一个线程的put的数据被覆盖。第二就是如果多个线程同时检测到元素个数超过数组大小*loadFactor，

这样就会发生多个线程同时对Node数组进行扩容，都在重新计算元素位置以及复制数据，但是最终只有一个线程扩容后的数组会赋给table，也就是说其他线程的都会丢失，

并且各自线程put的数据也丢失。

 

Hashtable： HashTable源码中是使用synchronized来保证线程安全的

public synchronized V get(Object key) {

​       // 省略实现

​    }

public synchronized V put(K key, V value) {

​    // 省略实现

​    }

在8中ConcurrentHashMap摒弃了Segment（锁段）的概念，而是启用了一种全新的方式实现,利用CAS算法

 

 

hashmap的put 方法线程不安全–“这两个key会添加到数组的同一个位置，这样最终就会发生其中一个线程的put的数据被覆盖”。

这个不能说明，put是线程不安全的，因为即便是线程安全的，它也会被覆盖。

 

其实ConcurrentHashMap的put方法跟普通的HashMap没什么区别，如果key相同，依然会覆盖。

要想达到不覆盖，我们可以使用putIfAbsent()方法。

 

 

HashMap为什么线程不安全：

我们假设有两个进程同时进行put操作，且让HashMap进行扩容，同时进入transfer方法  

 

 

 

HashMap的工作原理

 

HashMap基于hashing原理，我们通过put()和get()方法储存和获取对象。

当我们将键值对传递给put()方法时，它调用键对象的hashCode()方法来计算hashcode，然后找到bucket位置来储存值对象。

当获取对象时，通过键对象的equals()方法找到正确的键值对，然后返回值对象。

HashMap使用链表来解决碰撞问题，当发生碰撞了，对象将会储存在链表的下一个节点中。

HashMap在每个链表节点中储存键值对对象。

 

当两个不同的键对象的hashcode相同时会发生什么？

面试官可能会提醒他们有equals()和hashCode()两个方法，并告诉他们两个对象就算hashcode相同，但是它们可能并不相等。

它们会储存在同一个bucket位置的链表中。键对象的equals()方法用来找到键值对。

因为hashcode相同，所以它们的bucket位置相同，‘碰撞’会发生。因为HashMap使用链表存储对象，这个Entry(包含有键值对的Map.Entry对象)会存储在链表中。

 

如果两个键的hashcode相同，你如何获取值对象？

当我们调用get()方法，HashMap会使用键对象的hashcode找到bucket位置，然后获取值对象。两个值对象储存在同一个bucket，将会遍历链表直到找到值对象，HashMap在链表中存储的是键值对

其中一些记得这个重要知识点的面试者会说，找到bucket位置之后，会调用keys.equals()方法去找到链表中正确的节点，最终找到要找的值对象。完美的答案！

一些优秀的开发者会指出使用不可变的、声明作final的对象，并且采用合适的equals()和hashCode()方法的话，将会减少碰撞的发生，提高效率。

为什么String, Interger这样的wrapper类适合作为键？ String, Interger这样的wrapper类作为HashMap的键是再适合不过了，而且String最为常用。因为String是不可变的，也是final的，而且已经重写了equals()和hashCode()方法了。其他的wrapper类也有这个特点。不可变性是必要的，因为为了要计算hashCode()，就要防止键值改变，如果键值在放入时和获取时返回不同的hashcode的话，那么就不能从HashMap中找到你想要的对象。不可变性还有其他的优点如线程安全。如果你可以仅仅通过将某个field声明成final就能保证hashCode是不变的，那么请这么做吧。

 

不可变性使得能够缓存不同键的hashcode，这将提高整个获取对象的速度，使用String，Interger这样的wrapper类作为键是非常好的选择。

Map<key,value>  ,根据key的hashCode 得到 数组的位置，如果2个key，k1、k2的hashCode一样，但equals方法不一样，则同一位置，以链表的形式存在。

则 map.get(k1) 、 map.get(k2) 时，首先根据 k1、k2的hashcode 找到位置，是在统一位置，然后再根据k1、k2 的equals方法来遍历 统一位置的链表，得到 k1，k2的value

 

如果HashMap的大小超过了负载因子(load factor)定义的容量，怎么办？

HashMap默认的负载因子大小为0.75，也就是说，当一个map填满了75%的bucket时候，和其它集合类(如ArrayList等)一样，

将会创建原来HashMap大小的两倍的bucket数组，来重新调整map的大小，并将原来的对象放入新的bucket数组中。

这个过程叫作rehashing，因为它调用hash方法找到新的bucket位置。

你了解重新调整HashMap大小存在什么问题吗？”你可能回答不上来，这时面试官会提醒你当多线程的情况下，可能产生条件竞争(race condition)。

因为如果两个线程都发现HashMap需要重新调整大小了，它们会同时试着调整大小。

在调整大小的过程中，存储在链表中的元素的次序会反过来，因为移动到新的bucket位置的时候，HashMap并不会将元素放在链表的尾部，而是放在头部，

这是为了避免尾部遍历(tail traversing)。如果条件竞争发生了，那么就死循环了。

 

 

 

===============================================================================Collections.synchronizedList & CopyOnWriteArrayList===============================================================================

CopyOnWriteArrayList和Collections.synchronizedList是实现线程安全的列表的两种方式。两种实现方式分别针对不同情况有不同的性能表现，其中CopyOnWriteArrayList的写操作性能较差，而多线程的读操作性能较好。而Collections.synchronizedList的写操作性能比CopyOnWriteArrayList在多线程操作的情况下要好很多，而读操作因为是采用了synchronized关键字的方式，其读操作性能并不如CopyOnWriteArrayList。因此在不同的应用场景下，应该选择不同的多线程安全实现类。

 

Collections.synchronizedList：

public static <T> List<T> synchronizedList(List<T> list) {  

return (list instanceof RandomAccess ?  

​               new SynchronizedRandomAccessList<T>(list) :  

​               new SynchronizedList<T>(list));//根据不同的list类型最终实现不同的包装类。  

}  

SynchronizedList对部分操作加上了synchronized关键字以保证线程安全。但其iterator()操作还不是线程安全的。

 

 

import java.util.ArrayList;

import java.util.List;

public class Resource3 {

​    public static void main(String[] args) throws InterruptedException {

​        List<String> a = new ArrayList<String>();

​        a.add("a");

​        a.add("b");

​        a.add("c");

​        final ArrayList<String> list = new ArrayList<String>(

​                a);

​        Thread t = new Thread(new Runnable() {

​            int count = -1;

​            @Override

​            public void run() {

​                while (true) {

​                    list.add(count++ + "");

​                }

​            }

​        });

​        t.setDaemon(true);

​        t.start();

​        Thread.currentThread().sleep(3);

​        for (String s : list) {

​            System.out.println(s);

​        }

​    }

}

 

这段代码运行的时候就会抛出java.util.ConcurrentModificationException错误。这是因为主线程在遍历list的时候，子线程在向list中添加元素。

那么有没有办法在遍历一个list的时候，还向list中添加元素呢？办法是有的。就是java concurrent包中的CopyOnWriteArrayList。

CopyOnWriteArrayList类最大的特点就是，在对其实例进行修改操作（add/remove等）会新建一个数据并修改，修改完毕之后，再将原来的引用指向新的数组。这样，修改过程没有修改原来的数组。也就没有了ConcurrentModificationException错误。

 

 

 

 

 

 

 

 

 

 

 

 

===============================================================================Java hashCode() 和 equals()的若干问题解答===============================================================================

equals() 定义在JDK的Object.java中，通过判断两个对象的地址是否相等(即，是否是同一个对象)来区分它们是否相等

public boolean equals(Object obj) {

​    return (this == obj);

}

使用默认的“equals()”方法，等价于“==”方法。 因此，我们通常会重写equals()方法：String就重写了equals方法

private static class Person {

24         int age;

25         String name;

 

36         /**

37          * @desc 覆盖equals方法

38          */  

39         @Override

40         public boolean equals(Object obj){  

41             if(obj == null){  

42                 return false;  

43             }  

44               

45             //如果是同一个对象返回true，反之返回false  

46             if(this == obj){  

47                 return true;  

48             }  

49               

50             //判断是否类型相同  

51             if(this.getClass() != obj.getClass()){  

52                 return false;  

53             }  

54               

55             Person person = (Person)obj;  

56             return name.equals(person.name) && age==person.age;  

57         }

58     }

59 }

 

== : 它的作用是判断两个对象的地址是不是相等。即，判断两个对象是不试同一个对象。

equals() : 它的作用也是判断两个对象是否相等。但它一般有两种使用情况(前面第1部分已详细介绍过)：

​                 情况1，类没有覆盖equals()方法。则通过equals()比较该类的两个对象时，等价于通过“==”比较这两个对象。

​                 情况2，类覆盖了equals()方法。一般，我们都覆盖equals()方法来两个对象的内容相等；若它们的内容相等，则返回true(即，认为这两个对象相等)。

 

 

hashCode()：

hashCode() 的作用是获取哈希码，也称为散列码；它实际上是返回一个int整数。这个哈希码的作用是确定该对象在哈希表中的索引位置。

hashCode() 定义在JDK的Object.java中，这就意味着Java中的任何类都包含有hashCode() 函数。

但是，仅仅当创建并某个“类的散列表”时，该类的hashCode() 才有用

java集合中本质是散列表的类，如HashMap，Hashtable，HashSet。

也就是说：hashCode() 在散列表中才有用，在其它情况下没用。

我们都知道，散列表(HashMap)存储的是键值对(key-value)，它的特点是：能根据“键”快速的检索出对应的“值”。

散列表的本质是通过数组实现的。当我们要获取散列表中的某个“值”时，实际上是要获取数组中的某个位置的元素。

而数组的位置，就是通过“键”来获取的；更进一步说，数组的位置，是通过“键”对应的散列码计算得到的。

 

hashCode() 和 equals() 的关系:

我们不会在HashSet, Hashtable, HashMap等等这些本质是散列表的数据结构中，用到该类。例如，不会创建该类的HashSet集合。在这种情况下，该类的“hashCode() 和 equals() ”没有半毛钱关系的

这种情况下，equals() 用来比较该类的两个对象是否相等。而hashCode() 则根本没有任何作用，所以，不用理会hashCode()。

 

我们会在HashSet, Hashtable, HashMap等等这些本质是散列表的数据结构中，用到该类。例如，会创建该类的HashSet集合。

在这种情况下，该类的“hashCode() 和 equals() ”是有关系的：

​        1)、如果两个对象相等，那么它们的hashCode()值一定相同。

​              这里的相等是指，通过equals()比较两个对象时返回true。

​        2)、如果两个对象hashCode()相等，它们并不一定相等。

​              因为在散列表中，hashCode()相等，即两个键值对的哈希值相等。然而哈希值相等，并不一定能得出键值对相等。补充说一句：“两个不同的键值对，哈希值相等”，这就是哈希冲突。

在这种情况下。若要判断两个对象是否相等，除了要覆盖equals()之外，也要覆盖hashCode()函数。否则，equals()无效。

例如，创建Person类的HashSet集合，必须同时覆盖Person类的equals() 和 hashCode()方法。

 

 

public class ConflictHashCodeTest1{

11

12     public static void main(String[] args) {

13         // 新建Person对象，

14         Person p1 = new Person("eee", 100);

15         Person p2 = new Person("eee", 100);

16         Person p3 = new Person("aaa", 200);

17

18         // 新建HashSet对象

19         HashSet set = new HashSet();

20         set.add(p1);

21         set.add(p2);

22         set.add(p3);

23

24         // 比较p1 和 p2， 并打印它们的hashCode()

25         System.out.printf("p1.equals(p2) : %s; p1(%d) p2(%d)\n", p1.equals(p2), p1.hashCode(), p2.hashCode());

26         // 打印set

27         System.out.printf("set:%s\n", set);

28     }

29

30     /**

31      * @desc Person类。

32      */

33     private static class Person {

34         int age;

35         String name;

36

37         public Person(String name, int age) {

38             this.name = name;

39             this.age = age;

40         }

41

42         public String toString() {

43             return "("+name + ", " +age+")";

44         }

45

46         /**

47          * @desc 覆盖equals方法

48          */  

49         @Override

50         public boolean equals(Object obj){  

51             if(obj == null){  

52                 return false;  

53             }  

54               

55             //如果是同一个对象返回true，反之返回false  

56             if(this == obj){  

57                 return true;  

58             }  

59               

60             //判断是否类型相同  

61             if(this.getClass() != obj.getClass()){  

62                 return false;  

63             }  

64               

65             Person person = (Person)obj;  

66             return name.equals(person.name) && age==person.age;  

67         }

68     }

69 }

 

p1.equals(p2) : true; p1(1169863946) p2(1690552137)

set:[(eee, 100), (eee, 100), (aaa, 200)]

我们重写了Person的equals()。但是，很奇怪的发现：HashSet中仍然有重复元素：p1 和 p2。为什么会出现这种情况呢？

这是因为虽然p1 和 p2的内容相等，但是它们的hashCode()不等；所以，HashSet在添加p1和p2的时候，认为它们不相等。

 

也即：HashSet在添加元素时再判断是不是同一个对象时，是判断 equals  和 hashcode 2个方法。2个方法都一样，才认为这2个对象是重复的。

普通的判断2个元素是不是同一个对象，是判断 equals方法。

 

Object的hashCode()

Object类中hashCode()方法的声明如下：

public native int hashCode();

可以看出，hashCode()是一个native方法，而且返回值类型是整形；实际上，该native方法将对象在内存中的地址作为哈希码返回，可以保证不同对象的返回值不同。

 

（1）hashCode()在哈希表中起作用，如java.util.HashMap。

（2）如果对象在equals()中使用的信息都没有改变，那么hashCode()值始终不变。

（3）如果两个对象使用equals()方法判断为相等，则hashCode()方法也应该相等。

（4）如果两个对象使用equals()方法判断为不相等，则不要求hashCode()也必须不相等；但是开发人员应该认识到，不相等的对象产生不相同的hashCode可以提高哈希表的性能。

 

哈希表中起作用，如HashSet、HashMap等。

当我们向哈希表(如HashSet、HashMap等)中添加对象object时，首先调用hashCode()方法计算object的哈希码，

通过哈希码可以直接定位object在哈希表中的位置(一般是哈希码对哈希表大小取余)。如果该位置没有对象，可以直接将object插入该位置；

如果该位置有对象(可能有多个，通过链表实现)，则调用equals()方法比较这些对象与object是否相等，如果相等，则不需要保存object；如果不相等，则将该对象加入到链表中。

 

重写hashcode()的原则

通过前面的描述我们知道，重写hashCode需要遵守以下原则：

（1）如果重写了equals()方法，检查条件“两个对象使用equals()方法判断为相等，则hashCode()方法也应该相等”是否成立，如果不成立，则重写hashCode()方法。

（2）hashCode()方法不能太过简单，否则哈希冲突过多。

（3）hashCode()方法不能太过复杂，否则计算复杂度过高，影响性能。

 

 

 

 

 

 

 

 

 

 

 

 

===============================================================================callable和futureTask===============================================================================

Callable c = new Callable();

FutureTask<?>  task = new FutureTask<?> (c);

new Thread(task).start();

 

task.get();   返回结果，会一直等到有结果。

 

===============================================================================读写锁===============================================================================

读写锁，读写 写读 互斥

但不存在写锁比读锁优先。

如果一线程获取了读锁，这是写锁要等待，等读锁释放了，写锁才会继续。

如果一线程获取了写锁，这是读锁要等待，等写锁释放了，读锁才会继续。

 

===============================================================================同步方法===============================================================================

 

public synchronized void getXX(){}          此时的锁是调用此方法的对象 ，this

public static synchronized void getXX(){}   此时的锁是调用此类.class ,Class实例

 

===============================================================================线程池===============================================================================

为什么要用线程池？

如果不用线程池，需要频繁的创建销毁线程。  new Thread(Runnable r).start();  

如果用了线程池，就是固定的这几个线程(corepollsize maximumsize)来处理任务

 

线程池中已经有创建好了的线程，每个线程都能得到重用，且不是用完就销毁

 

线程池维护的是线程队列，队列中保存中所有等待状态的的线程。避免了创建和销毁的额外开销。

 

工具类： ExecutorService Executors.newFixedThreadPool(int i) : 固定大小的线程池

​                                  .newCached                 : 缓存线程池，大小是不固定的，根据需求自动的更改数量,创建一个不限线程数上限的线程池，任何提交的任务都将立即执行

​                                  .newSingle                 : 线程池中就一个线程

​                                  .newScheduled              : 线程池调度，延时 或 定时

 

ForkJoinPool  分支/合并 框架

 

 

Executors.newFixedThreadPool(int nThreads)，但是便捷不仅隐藏了复杂性，也为我们埋下了潜在的隐患（OOM，线程耗尽）。

小程序使用这些快捷方法没什么问题，对于服务端需要长期运行的程序，创建线程池应该直接使用ThreadPoolExecutor的构造方法。

 

线程池的工作顺序:

corePoolSize -> 任务队列 -> maximumPoolSize -> 拒绝策略

可以向线程池提交的任务有两种：Runnable和Callable，二者的区别如下：

方法签名不同，void Runnable.run(), V Callable.call() throws Exception

是否允许有返回值，Callable允许有返回值

是否允许抛出异常，Callable允许抛出异常。

 

不要使用Executors.newXXXThreadPool()快捷方法创建线程池，因为这种方式会使用无界的任务队列，为避免OOM，我们应该使用ThreadPoolExecutor的构造方法手动指定队列的最大长度：

 

任务队列总有占满的时候，这是再submit()提交新的任务会怎么样呢？RejectedExecutionHandler接口为我们提供了控制方式，接口定义如下：

public interface RejectedExecutionHandler {

​    void rejectedExecution(Runnable r, ThreadPoolExecutor executor);

}

 

线程池默认的拒绝行为是AbortPolicy，也就是抛出RejectedExecutionHandler异常，该异常是非受检异常，很容易忘记捕获。如果不关心任务被拒绝的事件，可以将拒绝策略设置成DiscardPolicy，这样多余的任务会悄悄的被忽略。

 

线程池的处理结果、以及处理过程中的异常都被包装到Future中，并在调用Future.get()方法时获取，执行过程中的异常会被包装成ExecutionException

 

ExecutorService executorService = Executors.newFixedThreadPool(4);

Future<Object> future = executorService.submit(new Callable<Object>() {

​        @Override

​        public Object call() throws Exception {

​            throw new RuntimeException("exception in call~");// 该异常会在调用Future.get()时传递给调用者

​        }

​    });

​     

try {

  Object result = future.get();

} catch (InterruptedException e) {

  // interrupt

} catch (ExecutionException e) {

  // exception in Callable.call()

  e.printStackTrace();

}

 

获取单个结果

过submit()向线程池提交任务后会返回一个Future，调用V Future.get()方法能够阻塞等待执行结果，V get(long timeout, TimeUnit unit)方法可以指定等待的超时时间。

 

 

获取多个结果

如果向线程池提交了多个任务，要获取这些任务的执行结果，可以依次调用Future.get()获得。但对于这种场景，我们更应该使用ExecutorCompletionService，该类的take()方法总是阻塞等待某一个任务完成，然后返回该任务的Future对象。向CompletionService批量提交任务后，只需调用相同次数的CompletionService.take()方法，就能获取所有任务的执行结果，获取顺序是任意的，取决于任务的完成顺序：

 

void solve(Executor executor, Collection<Callable<Result>> solvers)

   throws InterruptedException, ExecutionException {

​    

   CompletionService<Result> ecs = new ExecutorCompletionService<Result>(executor);// 构造器

​    

   for (Callable<Result> s : solvers)// 提交所有任务

​       ecs.submit(s);

​        

   int n = solvers.size();

   for (int i = 0; i < n; ++i) {// 获取每一个完成的任务

​       Result r = ecs.take().get();

​       if (r != null)

​           use(r);

   }

}

 

 

单个任务的超时时间

V Future.get(long timeout, TimeUnit unit)方法可以指定等待的超时时间，超时未完成会抛出TimeoutException。

 

多个任务的超时时间

等待多个任务完成，并设置最大等待时间，可以通过CountDownLatch完成：

public void testLatch(ExecutorService executorService, List<Runnable> tasks)

​    throws InterruptedException{

​       

​    CountDownLatch latch = new CountDownLatch(tasks.size());

​      for(Runnable r : tasks){

​          executorService.submit(new Runnable() {

​              @Override

​              public void run() {

​                  try{

​                      r.run();

​                  }finally {

​                      latch.countDown();// countDown

​                  }

​              }

​          });

​      }

​      latch.await(10, TimeUnit.SECONDS); // 指定超时时间

}

 

 

 

ExecutorService 接口的两个实现：ThreadPoolExecutor 和 ForkJoinPool。并且是 Java 7 中 fork/join 框架的重要组件。

fork/join 框架基于“工作窃取算法”。简而言之，意思就是执行完任务的线程可以从其他运行中的线程“窃取”工作。

ForkJoinPool 适用于任务创建子任务的情况，或者 外部客户端 创建大量 小任务 到线程池。

 

创建 ForkJoinTask 子类

根据某种条件将任务切分成子任务

调用执行任务

将任务结果合并

实例化对象并添加到池中

 

创建一个 ForkJoinTask，你可以选择 RecursiveAction 或 RecursiveTask 这两个子类，后者有返回值。

 

ThreadPoolExecutor 与 ForkJoinPool 对比

当选择线程池时，非常重要的一点是牢记创建、管理线程以及线程间切换执行会带来的开销。

ThreadPoolExecutor 可以控制线程数量和每个线程执行的任务。这很适合你需要在不同的线程上执行少量巨大的任务。

相比较而言，ForkJoinPool 基于线程从其他线程“窃取”任务。正因如此，当任务可以分割成小任务时可以提高效率。

为了实现工作窃取算法，fork/join 框架使用两种队列：

包含所有任务的主要队列

每个线程的任务队列

当线程执行完自己任务队列中的任务，它们试图从其他队列获取任务。为了使这一过程更加高效，线程任务队列使用双端队列（double ended queue）数据结构，一端与线程交互，另一端用于“窃取”任务。

最后要注意的一点 ForkJoinPool 只适用于任务可以创建子任务。否则它和 ThreadPoolExecutor 没区别，甚至开销更大。

 

 

ForkJoinPool的优势在于，可以充分利用多cpu，多核cpu的优势，把一个任务拆分成多个“小任务”，把多个“小任务”放到多个处理器核心上并行执行；当多个“小任务”执行完成之后，再将这些执行结果合并起来即可。这种思想值得学习。

Java7 提供了ForkJoinPool来支持将一个任务拆分成多个“小任务”并行计算，再把多个“小任务”的结果合并成总的计算结果。

ForkJoinPool是ExecutorService的实现类，因此是一种特殊的线程池。

使用方法：创建了ForkJoinPool实例之后，就可以调用ForkJoinPool的submit(ForkJoinTask<T> task) 或invoke(ForkJoinTask<T> task)方法来执行指定任务了。

其中ForkJoinTask代表一个可以并行、合并的任务。ForkJoinTask是一个抽象类，它还有两个抽象子类：RecusiveAction和RecusiveTask。其中RecusiveTask代表有返回值的任务，而RecusiveAction代表没有返回值的任务。

 

compute() 方法，用于合并每个子任务的结果。

 

以还行没有返回值的“大任务”（简单低打印1~300的数值）为例，程序将一个“大任务”拆分成多个“小任务”，并将任务交给ForkJoinPool来执行

例子：

public class PrintTask extends RecursiveAction {

​    private static final int THRESHOLD = 50; // 最多只能打印50个数

​    private int start;

​    private int end;

​    public PrintTask(int start, int end) {

​        super();

​        this.start = start;

​        this.end = end;

​    }

​    @Override

​    protected void compute() {

​        if (end - start < THRESHOLD) {

​            for (int i = start; i < end; i++) {

​                System.out.println(Thread.currentThread().getName() + "的i值：" + i);

​            }

​        } else {

​            int middle = (start + end) / 2;

​            PrintTask left = new PrintTask(start, middle);

​            PrintTask right = new PrintTask(middle, end);

​            // 并行执行两个“小任务”

​            left.fork();

​            right.fork();

​        }

​    }

}

 

public class ForkJoinPoolAction {

​    public static void main(String[] args) throws Exception {

​        PrintTask task = new PrintTask(0, 300);

​        // 创建实例，并执行分割任务

​        ForkJoinPool pool = new ForkJoinPool();

​        pool.submit(task);

​        // 线程阻塞，等待所有任务完成

​        System.out.println("end one " + System.currentTimeMillis());

​        pool.awaitTermination(2, TimeUnit.SECONDS);

​        System.out.println("end one2 " + System.currentTimeMillis());

​        pool.shutdown();

​    }

}

 

因为我的电脑是i7处理器，一共8个cpu，观察线程的名称可以发现，8个cpu都在运行。

 

 

 

通过RecursiveTask的返回值，来对一个长度为100的数组元素进行累加：

public class ForJoinPollTask {

​    public static void main(String[] args) throws Exception {

​        int[] arr = new int[100];

​        Random random = new Random();

​        int total =0;

​        //初始化100个数组元素

​        for(int i=0,len = arr.length;i<len;i++){

​            int temp = random.nextInt(20);

​            //对数组元素赋值，并将数组元素的值添加到sum总和中

​            total += (arr[i]=temp);

​        }

​        System.out.println("初始化数组总和："+total);

​        SumTask task = new SumTask(arr, 0, arr.length);

//      创建一个通用池，这个是jdk1.8提供的功能

​        ForkJoinPool pool = ForkJoinPool.commonPool();

​        Future<Integer> future = pool.submit(task); //提交分解的SumTask 任务

​        System.out.println("多线程执行结果："+future.get());

​        pool.shutdown(); //关闭线程池

​    }

}

 

class SumTask extends RecursiveTask<Integer>{

​    private static final int THRESHOLD = 20; //每个小任务 最多只累加20个数

​    private int arry[];

​    private int start;

​    private int end;

​    /**

​     \* Creates a new instance of SumTask.

​     \* 累加从start到end的arry数组

​     \* @param arry

​     \* @param start

​     \* @param end

​     */

​    public SumTask(int[] arry, int start, int end) {

​        super();

​        this.arry = arry;

​        this.start = start;

​        this.end = end;

​    }

​    @Override

​    protected Integer compute() {

​        int sum =0;

​        //当end与start之间的差小于threshold时，开始进行实际的累加

​        if(end - start <THRESHOLD){

​            for(int i= start;i<end;i++){

​                sum += arry[i];

​            }

​            return sum;

​        }else {//当end与start之间的差大于threshold，即要累加的数超过20个时候，将大任务分解成小任务

​            int middle = (start+ end)/2;

​            SumTask left = new SumTask(arry, start, middle);

​            SumTask right = new SumTask(arry, middle, end);

​            //并行执行两个 小任务

​            left.fork();

​            right.fork();

​            //把两个小任务累加的结果合并起来

​            return left.join()+right.join();   //invokeAll(left, right);   List<String> leftResult = task1.join();   List<String> rightResult = task2.join();

​        }

​    }

}

 

 

ForkJoinPool：

它使用了一个无限队列来保存需要执行的任务，而线程的数量则是通过构造函数传入，如果没有向构造函数中传入希望的线程数量，那么当前计算机可用的CPU数量会被设置为线程数量作为默认值。

orkJoinPool主要用来使用分治法(Divide-and-Conquer Algorithm)来解决问题。典型的应用比如快速排序算法。

 

比如要对1000万个数据进行排序，那么会将这个任务分割成两个500万的排序任务和一个针对这两组500万数据的合并任务。

以此类推，对于500万的数据也会做出同样的分割处理，到最后会设置一个阈值来规定当数据规模到多少时，停止这样的分割处理。比如，当元素的数量小于10时，会停止分割，转而使用插入排序对它们进行排序。

那么到最后，所有的任务加起来会有大概2000000+个。问题的关键在于，对于一个任务而言，只有当它所有的子任务完成之后，它才能够被执行。

所以当使用ThreadPoolExecutor时，使用分治法会存在问题，因为ThreadPoolExecutor中的线程无法像任务队列中再添加一个任务并且在等待该任务完成之后再继续执行。

而使用ForkJoinPool时，就能够让其中的线程创建新的任务，并挂起当前的任务，此时线程就能够从队列中选择子任务执行。

而使用ForkJoinPool时，就能够让其中的线程创建新的任务，并挂起当前的任务，此时线程就能够从队列中选择子任务执行。

而使用ForkJoinPool时，就能够让其中的线程创建新的任务，并挂起当前的任务，此时线程就能够从队列中选择子任务执行。

而使用ForkJoinPool时，就能够让其中的线程创建新的任务，并挂起当前的任务，此时线程就能够从队列中选择子任务执行。

ForkJoinPool ： 对于一个任务而言，只有当它所有的子任务完成之后，它才能够被执行。

 

以上程序的关键是fork()和join()方法。在ForkJoinPool使用的线程中，会使用一个内部队列来对需要执行的任务以及子任务进行操作来保证它们的执行顺序。 （join汇总）

那么使用ThreadPoolExecutor或者ForkJoinPool，会有什么性能的差异呢？

首先，使用ForkJoinPool能够使用数量有限的线程来完成非常多的具有父子关系的任务，比如使用4个线程来完成超过200万个任务。

但是，使用ThreadPoolExecutor时，是不可能完成的，因为ThreadPoolExecutor中的Thread无法选择优先执行子任务，需要完成200万个具有父子关系的任务时，也需要200万个线程，显然这是不可行的。

 

就比如两个CPU上有不同的任务，这时候A已经执行完，B还有任务等待执行，这时候A就会将B队尾的任务偷过来，加入自己的队列中，对于传统的线程，ForkJoin更有效的利用的CPU资源！

 

 

Fork/Join框架是Java 7提供的一个用于并行执行任务的框架，是一个把大任务分割成若干个小任务，最终汇总每个小任务结果后得到大任务结果的框架。

1.任务分割：首先Fork/Join框架需要把大的任务分割成足够小的子任务，如果子任务比较大的话还要对子任务进行继续分割

2.执行任务并合并结果：分割的子任务分别放到双端队列里，然后几个启动线程分别从双端队列里获取任务执行。子任务执行完的结果都放在另外一个队列里，启动一个线程从队列里取数据，然后合并这些数据。

 

 

Java 7的 ForkJoinPool 和Java8 的并行数据流（parallel Stream） 都对并行处理有所帮助

 

===============================================================================删除集合UnsupportedOperationException异常==================================================================List<String> lists = Arrays.asList("abc,def,g".split(","));

 

for(int k = 0; k < lists.size(); k++){

​    String str = lists.get(k);

​    if("def".equals(str)){

​        lists.remove(str);

​        k--;

​    }

}

 

经查看源码发现使用Arrays.asList返回的ArrayList是Arrays类中返回的，并不是ArrayList类中的，前者不支持remove方法。

List<String> lists = Arrays.asList("abc,def,g".split(","));

lists = new ArrayList<>(lists);

for(int k = 0; k < lists.size(); k++){

​    String str = lists.get(k);

​    if("def".equals(str)){

​        lists.remove(str);

​        k--;

​    }

}

 

===============================================================================ArrayList和LinkedList的区别以及优缺点===============================================================================

对于ArrayList，它在集合的末尾删除或添加元素所用的时间是一致的，但是在列表中间的部分添加或删除时所用时间就会大大增加。但是它在根据索引查找元素的时候速度很快。

 

对于LinkedList则相反，它在插入、删除集合中任何位置的元素所花费的时间都是一样的，但是它根据索引查询一个元素的时候却比较慢。

1.ArrayList是实现了基于动态数组的数据结构，LinkedList是基于链表结构。

2.对于随机访问的get和set方法，ArrayList要优于LinkedList，因为LinkedList要移动指针。

3.对于新增和删除操作add和remove，LinkedList比较占优势，因为ArrayList要移动数据。

 

1.对ArrayList和LinkedList而言，在列表末尾增加一个元素所花的开销都是固定的。对 ArrayList而言，主要是在内部数组中增加一项，指向所添加的元素，偶尔可能会导致对数组重新进行分配；而对LinkedList而言，这个开销是 统一的，分配一个内部Entry对象。

2.在ArrayList集合中添加或者删除一个元素时，当前的列表所所有的元素都会被移动。而LinkedList集合中添加或者删除一个元素的开销是固定的。

3.LinkedList集合不支持 高效的随机随机访问（RandomAccess），因为可能产生二次项的行为。

4.ArrayList的空间浪费主要体现在在list列表的结尾预留一定的容量空间，而LinkedList的空间花费则体现在它的每一个元素都需要消耗相当的空间

 

 

===============================================================================有序 无序=========================================================

\* Collection

\* |--List

\* 有序(存储顺序和取出顺序一致),可重复

\* |--Set

\* 无序(存储顺序和取出顺序不一致),唯一

由于SET是按hash存储数据，所以存储顺序和取出顺序不一致

删除List中重复元素，并保持顺序：

public static <T> List<T> removeDuplicateKeepOrder(List<T> list){

​    Set set = new HashSet();

​    List<T> newList = new ArrayList<>();

​    for (T element : list) {

​        //set能添加进去就代表不是重复的元素

​        if (set.add(element)) newList.add(element);

​    }

​    list.clear();

​    list.addAll(newList);

​    return list;

}

 

=======================================================================获取客户端的IP=======================================================================

 

​     \* 功能描述：获取客户端的IP

​     *

​     \* @param request 请求参数

​     \* @return 返回客户端IP

​     */

​    public static String getRemortIP(HttpServletRequest request) {

​        if (request.getHeader("x-forwarded-for") == null) {

​            return request.getRemoteAddr();

​        }

​        return request.getHeader("x-forwarded-for");

​    }

}

==============================================================================InitializingBean============================================================

public interface InitializingBean {

​    void afterPropertiesSet() throws Exception;

}

 

InitializingBean 与 init-method 的区别

 

InitializingBean接口为bean提供了初始化方法的方式，它只包括afterPropertiesSet方法，凡是继承该接口的类，在初始化bean的时候会执行该方法。

在spring初始化bean的时候，如果该bean是实现了InitializingBean接口，并且同时在配置文件中指定了init-method，系统则是先调用afterPropertiesSet方法，然后在调用init-method中指定的方法。

2：实现InitializingBean接口是直接调用afterPropertiesSet方法，比通过反射调用init-method指定的方法效率相对来说要高点。但是init-method方式消除了对spring的依赖

3：如果调用afterPropertiesSet方法时出错，则不调用init-method指定的方法。

==============================================================================拦截器(Interceptor)   过滤器   监听器============================================================

HandlerInterceptor 接口

HandlerInterceptorAdapter 类

拦截器的拦截是基于反射机制实现的，拦截的对象只能是实现了借口的类，不能拦截url这种链接

 

自定义拦截器的步骤

​    第一步：自定义一个实现了Interceptor接口的类，或者继承抽象类AbstractInterceptor。

​    第二步：在配置文件中注册定义的拦截器。

​    第三步：在需要使用Action中引用上述定义的拦截器，为了方便也可以将拦截器定义为默认的拦截器，这样在不加特殊说明的情况下，所有的Action都被这个拦截器拦截。

​    

过滤器Filter与拦截器Interceptor的区别：

​    过滤器可以简单的理解为“取你所想取”，过滤器关注的是web请求；拦截器可以简单的理解为“拒你所想拒”，拦截器关注的是方法调用，比如拦截敏感词汇。

4.1，拦截器是基于java反射机制来实现的，而过滤器是基于函数回调来实现的。（有人说，拦截器是基于动态代理来实现的）

4.2，拦截器不依赖servlet容器，过滤器依赖于servlet容器。

4.3，拦截器只对Action起作用，过滤器可以对所有请求起作用。

4.4，拦截器可以访问Action上下文和值栈中的对象，过滤器不能。

4.5，在Action的生命周期中，拦截器可以多次调用，而过滤器只能在容器初始化时调用一次。

 

============================================================================protected==============================================================

public private(本类)   protected(不限包名的子类 + 本包中)    default(本包)   

protected 修饰的方法与属性

 

 

=======================================================================根据实体类中的Column注解转为map===================================================================

/**

​     \* 功能描述：解析方法<br>

​     \* 根据实体类中的Column注解转为map

​     \* 输入参数：Object类型<按照参数定义顺序>

​     \* @param entity

​     \* 返回值:  map类型 <说明>

​     \* @return  Map<String, Object>

​     \* @throw 异常描述

​     \* @see 需要参见的其它内容

​     */

​    public static Map<String, Object> parser(Object entity) {

​        Map<String, Object> values = new HashMap<String, Object>();

​        Method[] methods = entity.getClass().getMethods();

​        for (Method method : methods) {

​            if (method.isAnnotationPresent(Column.class)) {

​                Column column = method.getAnnotation(Column.class);

​                PropertyDescriptor descriptor = BeanUtils.findPropertyForMethod(method);

​                String key = descriptor.getName();

​                Object value = null;

​                try {

​                    value = method.invoke(entity, new Object[] {});

​                    if (value instanceof java.util.Date) {

​                        value = dateFormat(column, (Date) value);

​                    }

​                } catch (Exception e) {

​                    logger.debug("reflect error.[" + method + "]", e);

​                }

​                values.put(key, value);

​            }

​        }

​        return values;

​    }

​        private static Object dateFormat(Column column, Date date) {

​        if (date != null && !"".equals(column.columnDefinition())) {

​            SimpleDateFormat format = new SimpleDateFormat(column.columnDefinition());

​            return format.format(date);

​        }

​        return date;

​    }

 

=======================================================================Bean转换为Map=======================================================================

public static Map<String, Object> transBean2Map(Object obj) {

​        if (obj == null) {

​            return null;

​        }

​        Map<String, Object> map = new HashMap<String, Object>();

​        try {

​            BeanInfo beanInfo = Introspector.getBeanInfo(obj.getClass());

​            PropertyDescriptor[] propertyDescriptors = beanInfo.getPropertyDescriptors();

​            for (PropertyDescriptor property : propertyDescriptors) {

​                String key = property.getName();

​                // 过滤class属性

​                if (!key.equals("class")) {

​                    // 得到property对应的getter方法

​                    Method getter = property.getReadMethod();

​                    Object value = getter.invoke(obj);

​                    map.put(key, value);

​                }

​            }

​        } catch (Exception e) {

​            logger.debug("transBean2Map Error " + e);

​        }

​        return map;

}    

 

 

// 获取beal的set方法

// Method writeme = property.getWriteMethod();

=======================================================================Java内省机制IntroSpector==================================================================

内省(IntroSpector)是Java语言对JavaBean 类属性、事件的一种处理方法。Apache BeanUtils 具有更高级的Bean操作功能，比如 级联属性 操作。

 

public class Book {

​    private int id;

 

​    private long price;

 

​    private String name;

 

​    private Date date;

}

BeanInfo beanInfo = Introspector.getBeanInfo(obj.getClass());

PropertyDescriptor[] propertyDescriptors = beanInfo.getPropertyDescriptors();    

 

propertyDescriptors:

[java.beans.PropertyDescriptor[name=class; propertyType=class java.lang.Class; readMethod=public final native java.lang.Class java.lang.Object.getClass()], java.beans.PropertyDescriptor[name=date; propertyType=class java.util.Date; readMethod=public java.util.Date webin.operationanalysis.controller.Book.getDate(); writeMethod=public void webin.operationanalysis.controller.Book.setDate(java.util.Date)],

java.beans.PropertyDescriptor[name=id; propertyType=int; readMethod=public int webin.operationanalysis.controller.Book.getId(); writeMethod=public void webin.operationanalysis.controller.Book.setId(int)],

java.beans.PropertyDescriptor[name=name; propertyType=class java.lang.String; readMethod=public java.lang.String webin.operationanalysis.controller.Book.getName(); writeMethod=public void webin.operationanalysis.controller.Book.setName(java.lang.String)],

java.beans.PropertyDescriptor[name=price; propertyType=long; readMethod=public long webin.operationanalysis.controller.Book.getPrice(); writeMethod=public void webin.operationanalysis.controller.Book.setPrice(long)]]

 

 

 

apache commons BeanUtils:

BeanUtils主要是封装了java反射(reflection)和自省（introspection）API，来对javabean进行操作。

https://blog.csdn.net/u011079274/article/details/52243940

 

 

​    

=======================================================================ServletContextListener=======================================================================

当Servlet 容器启动或终止Web 应用时，会触发ServletContextEvent 事件，该事件由ServletContextListener 来处理

例一：在服务启动时，将数据库中的数据加载进内存，并将其赋值给一个属性名，其它的 Servlet 就可以通过 getAttribute 进行属性值的访问。

1、ServletContext 对象是一个为整个 web 应用提供共享的内存，任何请求都可以访问里面的内容

​     public void contextInitialized(ServletContextEvent sce) {  

​         ServletContext sct=sce.getServletContext();

​    }

在完成上述编码后，仍需在 web.xml 中进行如下配置，以使得该监听器可以起作用。

<listener>

​    <listener-class>XXX.XXX.ServletContextLTest</listener-class>  

</listener>  

 

例二：书写一个类用于统计当Web 应用启动后，网页被客户端访问的次数。如果重新启动Web 应用，计数器不会重新从1 开始统计访问次数，而是从上次统计的结果上进行累加

 

 

=======================================================================HttpSessionListener=======================================================================

HttpSessionListener定义的两个方法：sessionCreated()和sessionDestroyed()。这两个方法可以监听到当前应用中session的创建和销毁情况。   当前应用！！！  当前应用!!!  当前应用!!!

web.xml:

​    <listener>

​        <listener-class>com.suning.lbi.impl.listener.SessionListener</listener-class>

​    </listener>

 

public class SessionListener implements HttpSessionListener  {

​     // 统计在线人数功能  

​    static int online ;//记录在线人数

​    public static final String onlineKey="onlineNumber";//redis中存储在线人数的的键

​    @Override

​    public void sessionCreated(HttpSessionEvent arg0) {

​        logger.info("单个session创建，用户在线总数量："+RedisCache.incrBy(onlineKey,1));

​        online++;

​    }

 

​    @Override

​    public void sessionDestroyed(HttpSessionEvent arg0) {

​        logger.info("单个session销毁，用户在线总数量："+RedisCache.incrBy(onlineKey,-1));

​        online--;

​    }

}

​    

以下两种情况下就会发生sessionDestoryed（会话销毁）事件：

执行session.invalidate()方法时。

既然LogoutServlet.java中执行session.invalidate()时，会触发sessionDestory()从在线用户列表中清除当前用户，我们就不必在LogoutServlet.java中对在线列表进行操作了，所以LogoutServlet.java的内容现在是这样。

 

public void doGet(HttpServletRequest request,HttpServletResponse response) throwsServletException, IOException {

​    // 销毁

​    session request.getSession().invalidate();

​    // 成功

​    response.sendRedirect("index.jsp");

}

如果用户长时间没有访问服务器，超过了会话最大超时时间，服务器就会自动销毁超时的session。

会话超时时间可以在web.xml中进行设置，为了容易看到超时效果，我们将超时时间设置为最小值。

<session-config> <session-timeout>1</session-timeout> </session-config>

时间单位是一分钟，并且只能是整数，如果是零或负数，那么会话就永远不会超时。    

​        

​    

=======================================================================HttpServletRequestWrapper=======================================================================

Wrapper：包装者

​    

Filter能在request到达servlet的服务方法之前拦截HttpServletRequest对象，而在服务方法转移控制后又能拦截HttpServletResponse对象。    

但HttpServletRequest对象的参数是不可改变的，这极大地缩减了filter的应用范围。但你却可以通过使用装饰模式来改变其状态    

​    

​    

=======================================================================XSS  攻击=======================================================================

public class XssHttpWrapper extends HttpServletRequestWrapper {

 

​    private HttpServletRequest orgRequest;

 

​    public XssHttpWrapper(HttpServletRequest request) {

​        super(request);

​        orgRequest = request;

​    }

 

​    @Override

​    public Map getParameterMap() {

​        Map<String, String[]> map = super.getParameterMap();

​        Map<String, String[]> newmap = new HashMap<String, String[]>();

​        String[] valueStrs;

​        for (Entry<String, String[]> entry : map.entrySet()) {

​            valueStrs = new String[entry.getValue().length];

​            for (int i = 0; i < entry.getValue().length; i++) {

 

​                valueStrs[i] = xssEncode(entry.getValue()[i]);

​            }

​            newmap.put(xssEncode(entry.getKey()), valueStrs);

​        }

​        return newmap;

​    }

 

​    /**

​     \* 覆盖getParameter方法，将参数名和参数值都做xss过滤。<br/>

​     \* 如果需要获得原始的值，则通过super.getParameterValues(name)来获取<br/>

​     \* getParameterNames,getParameterValues和getParameterMap也可能需要覆盖

​     */

​    @Override

​    public String getParameter(String name) {

​        String value = super.getParameter(xssEncode(name));

​        if (value != null) {

​            value = xssEncode(value);

​        }

​        return value;

​    }

 

​    /**

​     \* 覆盖getHeader方法，将参数名和参数值都做xss过滤。<br/>

​     \* 如果需要获得原始的值，则通过super.getHeaders(name)来获取<br/>

​     \* getHeaderNames 也可能需要覆盖

​     */

​    @Override

​    public String getHeader(String name) {

​        String value = super.getHeader(xssEncode(name));

​        if (value != null) {

​            value = xssEncode(value);

​        }

​        return value;

​    }

 

​    /**

​     \* 将容易引起xss漏洞的半角字符直接替换成全角字符

​     *

​     \* @param s

​     \* @return

​     */

​    private static String xssEncode(String s) {

​        if (s == null || s.isEmpty()) {

​            return s;

​        }

 

​        s = s.replaceAll("", "");

​        Pattern scriptPattern = [Pattern.compile](http://pattern.compile/)("<javascript>", Pattern.CASE_INSENSITIVE);

​        s = scriptPattern.matcher(s).replaceAll("");

​        scriptPattern = [Pattern.compile](http://pattern.compile/)("</javascript>", Pattern.CASE_INSENSITIVE);

​        s = scriptPattern.matcher(s).replaceAll("");

​        scriptPattern = [Pattern.compile](http://pattern.compile/)("<script>", Pattern.CASE_INSENSITIVE);

​        s = scriptPattern.matcher(s).replaceAll("");

​        scriptPattern = [Pattern.compile](http://pattern.compile/)("</script>", Pattern.CASE_INSENSITIVE);

​        s = scriptPattern.matcher(s).replaceAll("");

​        scriptPattern = Pattern.compile("&", Pattern.CASE_INSENSITIVE);

​        s = scriptPattern.matcher(s).replaceAll("&amp;");

​        scriptPattern = [Pattern.compile](http://pattern.compile/)("<", Pattern.CASE_INSENSITIVE);

​        s = scriptPattern.matcher(s).replaceAll("&lt;");

​        scriptPattern = [Pattern.compile](http://pattern.compile/)(">", Pattern.CASE_INSENSITIVE);

​        s = scriptPattern.matcher(s).replaceAll("&gt;");

​        scriptPattern = [Pattern.compile](http://pattern.compile/)("\"", Pattern.CASE_INSENSITIVE);

​        s = scriptPattern.matcher(s).replaceAll("&quot;");

​        return s;

​    }

 

​    /**

​     \* 获取最原始的request

​     *

​     \* @return

​     */

​    public HttpServletRequest getOrgRequest() {

​        return orgRequest;

​    }

 

​    /**

​     \* 获取最原始的request的静态方法

​     *

​     \* @return

​     */

​    public static HttpServletRequest getOrgRequest(HttpServletRequest req) {

​        if (req instanceof XssHttpWrapper) {

​            return ((XssHttpWrapper) req).getOrgRequest();

​        }

​        return req;

​    }

 

}

 

public class XssHttpFilter extends OncePerRequestFilter {

​    protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain filterChain) throws ServletException, IOException {

​        String uri = request.getRequestURI();

​        //scm中开启了xss拦截，并且不在白名单中，进行xss防护

​        if(ScmParams.xssStatus && ScmParams.xssSet!=null && !ScmParams.xssSet.contains(uri.substring(11))){

​            filterChain.doFilter(new XssHttpWrapper(request), response);

​        }else{

​            filterChain.doFilter(request, response);

​        }

​    }

}

 

web.xml:

​    <filter>

​        <filter-name>xssFilter</filter-name>

​        <filter-class>com.suning.lbi.xss.XssHttpFilter</filter-class>

​    </filter>

​    <filter-mapping>

​        <filter-name>xssFilter</filter-name>  

​        <url-pattern>*.action</url-pattern>

​    </filter-mapping>

 

 

=======================================================================抽象类=======================================================================     

抽象类不一定要有抽象方法。可以没有，也可以有，

一定要记住即使只有一个方法是abstract，整个类就必须定义成抽象的，

抽象类没有构造方法

可以把非抽象方法放在抽象类里面，同上第一行

 

 

 

=======================================================================动态代理=======================================================================

代理有点像 不需要修改源代码 来在源代码上增加一些功能。

说的高深一点，这就是“开闭原则”（可不是一开一闭的意思哦），它是设计模式中一条非常重要的原则，意思就是“对扩展开放，对修改封闭”。

 

静态代理：

若代理类在程序运行前就已经存在，那么这种代理方式被成为 静态代理 ，这种情况下的代理类通常都是我们在Java代码中定义的。

通常情况下， 静态代理中的代理类和委托类会实现同一接口或是派生自相同的父类

 

动态代理：

代理类在程序运行时创建的代理方式被成为 动态代理。

相比于静态代理， 动态代理的优势在于可以很方便的对代理类的函数进行统一的处理，而不用修改每个代理类的函数。

 

假设我们要实现这样一个需求：在执行委托类中的方法之前输出“before”，在执行完毕后输出“after”。

我们还是以上面例子中的Vendor类作为委托类，BusinessAgent类作为代理类来进行介绍。首先我们来使用静态代理来实现这一需求，相关代码如下：

public interface Sell { void sell(); void ad(); }

public class Vendor implements Sell {

   public void sell() {

​        System.out.println("In sell method");

   }

   public void ad() {

​        System.out.println("ad method")

   }

}

public class BusinessAgent implements Sell {

​        private Vendor mVendor;

​        public BusinessAgent(Vendor vendor) {

​            this.mVendor = vendor;

​        }

​        public void sell() {

​            System.out.println("before");

​            mVendor.sell();

​            System.out.println("after");

​        }

​        public void ad() {

​            System.out.println("before");

​            mVendor.ad();

​            System.out.println("after");

​        }

}

通过静态代理实现我们的需求需要我们在每个方法中都添加相应的逻辑，这里只存在两个方法所以工作量还不算大，假如Sell接口中包含上百个方法呢?这时候使用静态代理就会编写许多冗余代码。

通过使用动态代理，我们可以做一个“统一指示”，从而对所有代理类的方法进行统一处理，而不用逐一修改每个方法。

(1)InvocationHandler接口    //JDK自带

在使用动态代理时，我们需要定义一个位于代理类与委托类之间的中介类，这个中介类被要求实现InvocationHandler接口，这个接口的定义如下：

public interface InvocationHandler {

​    Object invoke(Object proxy, Method method, Object[] args);

}

当我们调用代理类对象的方法时，这个“调用”会转送到invoke方法中，代理类对象作为proxy参数传入，参数method标识了我们具体调用的是代理类的哪个方法，args为这个方法的参数。

我们对代理类中的所有方法的调用都会变为对invoke的调用，这样我们可以在invoke方法中添加统一的处理逻辑(也可以根据method参数对不同的代理类方法做不同的处理)

public interface Sell { void sell(); void ad(); }

public class Vendor implements Sell {

   public void sell() {

​       System.out.println("In sell method");

   }

   public void ad() {

​       System,out.println("ad method")

   }

}

//中介类

public class DynamicProxy implements InvocationHandler {

   private Object obj; //obj为委托类对象;

   public DynamicProxy(Object obj) {

​       this.obj = obj;

   }

​    @Override

​    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {

​          System.out.println("before");

​          Object result = method.invoke(obj, args);

​          System.out.println("after");

​          return result;

​     }

}

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!中介类持有一个委托类对象引用

我们调用Proxy类的newProxyInstance方法来获取一个代理类实例。这个代理类实现了我们指定的接口并且会把方法调用分发到指定的调用处理器。

 

public static void main(String[] args) {

​    // 创建中介类实例

​    DynamicProxy inter = new DynamicProxy(new Vendor());

​    // 加上这句将会产生一个$Proxy0.class文件，这个文件即为动态生成的代理类文件

​    System.getProperties().put("sun.misc.ProxyGenerator.saveGeneratedFiles", "true");

​    // 获取代理类实例sell

​    Sell sell = (Sell) (Proxy.newProxyInstance(Sell.class.getClassLoader(), new Class[] { Sell.class }, inter));

​    // 通过代理类对象调用代理类方法，实际上会转到invoke方法调用

​    sell.sell();

​    sell.ad();

}

 

Proxy.newProxyInstance：

public static Object newProxyInstance(ClassLoader loader, Class<?>[] interfaces, InvocationHandler h) throws IllegalArgumentException

loader：定义了代理类的ClassLoder;

interfaces：代理类实现的接口列表

h：调用处理器，也就是我们上面定义的实现了InvocationHandler接口的类实例

 

！！！！！！！！！！！！！！！！！！！！！！！！！！！！！

简单的总结下：首先通过newProxyInstance方法获取代理类实例，而后我们便可以通过这个代理类实例调用代理类的方法，

对代理类的方法的调用实际上都会调用中介类(调用处理器)的invoke方法，在invoke方法中我们调用委托类的相应方法，并且可以添加自己的处理逻辑。

！！！！！！！！！！！！！！！！！！！！！！！！！！！！！

 

代理模式最大的特点就是代理类和实际业务类实现同一个接口（或继承同一父类），代理对象持有一个实际对象的引用，外部调用时操作的是代理对象，而在代理对象的内部实现中又会去调用实际对象的操作

 

例子：

比如我们在应用中有这样一个需求，在对某个类的一个方法的调用前和调用后都要做一下日志操作，

一个普通的接口：

public interface AppService {  

​      public boolean createApp(String name);  

}  

public class AppServiceImpl implements AppService {  

​    public boolean createApp(String name) {  

​        System.out.println("App["+name+"] has been created.");  

​        return true;  

​    }  

}  

public class LoggerInterceptor implements InvocationHandler {//注意实现这个Handler接口  

​    private Object target;//目标对象的引用，这里设计成Object类型，更具通用性  

​    public LoggerInterceptor(Object target){  

​        this.target = target;  

​    }  

​    public Object invoke(Object proxy, Method method, Object[] arg)  

​            throws Throwable {  

​        System.out.println("Entered "+target.getClass().getName()+"-"+method.getName()+",with arguments{"+arg[0]+"}");  

​        Object result = method.invoke(target, arg);//调用目标对象的方法  

​        System.out.println("Before return:"+result);  

​        return result;  

​    }  

}  

public class Main {  

​    public static void main(String[] args) {  

​        AppService target = new AppServiceImpl();//生成目标对象  

​        //接下来创建代理对象  

​        AppService proxy = (AppService) Proxy.newProxyInstance(  

​                target.getClass().getClassLoader(),  

​                target.getClass().getInterfaces(), new LoggerInterceptor(target));  

​        proxy.createApp("Kevin Test");  

​    }  

}  

 

=======================================================================Proxy 遇上 Decorator=======================================================================

代理模式（Proxy 模式）可理解为：我想做，但不能做，我需要有一个能干的人来帮我做。

装饰器模式（Decorator 模式）可理解为：我想做，但不能做，我需要有各类特长的人来帮我做，但我有时只需要一个人，有时又需要很多人。

它们的区别就是，Proxy 模式需要的是一个能人，而 Decorator 模式需要的是一个团队。

 

想必您已经了解到 Proxy 模式与 Decorator 模式的本质区别了吧？

这里两个模式都是对类的包装，在不改变类自身的情况下，为其添加特定的功能。若这些功能比较单一，可考虑使用 Proxy 模式，但对于功能较多且需动态扩展的情况下，您不妨尝试一下 Decorator 模式吧！

 

Proxy：

public interface Greeting {

 

​    void sayHello(String name);

}

public class GreetingImpl implements Greeting {

 

​    @Override

​    public void sayHello(String name) {

​        System.out.println("Hello! " + name);

​    }

}

public class GreetingProxy implements Greeting {

 

​    private GreetingImpl greetingImpl;

 

​    public GreetingProxy(GreetingImpl greetingImpl) {

​        this.greetingImpl = greetingImpl;

​    }

 

​    @Override

​    public void sayHello(String name) {

​        before();

​        greetingImpl.sayHello(name);

​    }

 

​    private void before() {

​        System.out.println("Before");

​    }

}

 

public static void main(String[] args) {

​    Greeting greeting = new GreetingProxy(new GreetingImpl());

​    greeting.sayHello("Jack");

}

 

 

Decorator：

装饰器：

public abstract class GreetingDecorator implements Greeting {

​    private Greeting greeting;

 

​    public GreetingDecorator(Greeting greeting) {

​        this.greeting = greeting;

​    }

 

​    @Override

​    public void sayHello(String name) {

​        greeting.sayHello(name);

​    }

}

 

第一个具体装饰器 GreetingBefore：

public class GreetingBefore extends GreetingDecorator {

​    public GreetingBefore(Greeting greeting) {

​        super(greeting);

​    }

 

​    @Override

​    public void sayHello(String name) {

​        before();

​        super.sayHello(name);

​    }

 

​    private void before() {

​        System.out.println("Before");

​    }

}

 

第二个具体装饰器 GreetingAfter：

public class GreetingAfter extends GreetingDecorator {

​    public GreetingAfter(Greeting greeting) {

​        super(greeting);

​    }

 

​    @Override

​    public void sayHello(String name) {

​        super.sayHello(name);

​        after();

​    }

 

​    private void after() {

​        System.out.println("After");

​    }

}

 

public static void main(String[] args) {

​    Greeting greeting = new GreetingAfter(new GreetingBefore(new GreetingImpl()));

​    greeting.sayHello("Jack");

}

 

=======================================================================百度 echarts=======================================================================

统计的项目要做，在前端的数据需要用图表的形式展示 数据分析的模块，用到了echarts这个插件

官网： [http://echarts.baidu.com](http://echarts.baidu.com/)

​       http://echarts.baidu.com/echarts2/doc/example.html

1.引入js

<script src="/public/dist/js/echarts.js"></script>

2.在dom中插入chart

<div id="pie">

  <div id="pieChart"
style="width:650px;height:300px;"</div>

</div>

3.初始化chart

var myChartNum = echarts.init(document.getElementById("pieChart"));

4.初始化配置     去官网查

option = {

​    title : {

​        text: '某地区蒸发量和降水量',

​        subtext: '纯属虚构'

​    }

​    。。。。。。。

}

5.填充chart

myChartNum.setOption(option);

 

 

例子：

date ： ["2018-09-11", "2018-09-12", "2018-09-13", "2018-09-14", "2018-09-15", "2018-09-16", "2018-09-17", "2018-09-18", "2018-09-19", "2018-09-20"]

data ： [0, 0, 0, 0, 0, 0, 0, 4492, 0, 10189]

function skOrderQuaLine(date,data){

​    var myCheart = echarts.init(document.getElementById('sk_ddl'));

​    option = {

​            tooltip : {

​                trigger: 'axis',

​                formatter:function(a){

​                    var label = '<div class="shjy-chart-box-tipe">'+

​                                    '<div class="shjy-chart-box-tipe-name">' + a[0].name +'</div>' +

​                                    '<div id="yhmyd" class="shjy-chart-box-tipe-valu">' + a[0].value +  

​                                    '</div>'

​                                '</div>'

​                    return label

​                },

​                backgroundColor: '#ffffff',

​                extraCssText: 'box-shadow: 0px 0px 4px 0px rgba(178,178,178,0.5) '  

​            },

​            grid: {

​                top: 0,

​                bottom: 0,

​                left: 0,

​                right: 0

​            },

​            xAxis: {

​                type: 'category',

​                show:false,

​                data: date

​            },

​            yAxis:[{

​                type: 'value',

​                show:false,

​                scale: true,

​                axisLabel:{

​                    show:false

​                },

​                axisTick: {

​                    show:false

​                }

​            }],

​            series: [{

​                name: '当日落单量',

​                type: 'line',

​                smooth:true,

​                itemStyle:{

​                        normal:{

​                               color: '#68a5fa'

​                        }

​                },

​                symbol:'none', /*去除拐点*/

​                data: data,

​                areaStyle: {

​                    normal: {

​                         color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{

​                             offset: 0,

​                             color: 'rgb(220, 235, 255)'

​                         }, {

​                             offset: 1,

​                             color: 'rgb(255, 255, 255)'

​                         }])

​                     }

​                }

​                

​            }]

​        };

​        myCheart.setOption(option);

}

 

​    

=======================================================================mysql的coalesce使用技巧=======================================================================

今天无意间发现mysql的coalesce，

coalesce()解释：返回参数中的第一个非空表达式（从左向右依次类推）；

使用示例：a,b,c三个变量。

select coalesce(null,2,3); // Return 2

select coalesce(null,null,3); // Return 3

select coalesce(1,2,3); // Return 1

​    

​    

=======================================================================分布式架构=======================================================================

分布式系统（distributed system）是建立在网络之上的软件系统。

内聚性是指每一个数据库分布节点高度自治，有本地的数据库管理系统。透明性是指每一个数据库分布节点对用户的应用来说都是透明的，看不出是本地还是远程。

 

 

应用:

分布式文件系统，分布式缓存系统，分布式数据库，分布式WebService，分布式计算

分布式文件系统： 出名的有 Hadoop 的HDFS ,还有 google的 GFS , 淘宝的 TFS 等

分布式缓存系统：memcache , hbase , mongdb 等

分布式数据库 ： MySQL , Mariadb, PostgreSQL

分布式MySQL中间件-Mycat，来处理大并发大数据量的构架。

以及分布式相关的技术，分布式一致性ZooKeeper服务, 高可用HAProxy/keepalived等相关应用。

1> 集群 与 分布式

2> 负载均衡

3> 分布式相关的高可用、容灾等名词解释

4> Mycat 中间件学习

 

首先推荐4本书

大型分布式网站架构设计与实践

http://item.jd.com/11529266.html

大型网站技术架构：核心原理与案例分析

http://item.jd.com/11322972.html

大型网站系统与Java中间件实践

http://item.jd.com/11449803.html

分布式Java应用：基础与实践

http://item.jd.com/10144196.html

 

 

分布式架构下系统间交互的5种通信模式

request/response模式（同步模式）：客户端发起请求一直阻塞到服务端返回请求为止。

Callback（异步模式）：客户端发送一个RPC请求给服务器，服务端处理后再发送一个消息给消息发送端提供的callback端点，此类情况非常合适以下场景：A组件发送RPC请求给B，B处理完成后，需要通知A组件做后续处理。

Future模式：客户端发送完请求后，继续做自己的事情，返回一个包含消息结果的Future对象。客户端需要使用返回结果时，使用Future对象的.get(),如果此时没有结果返回的话，会一直阻塞到有结果返回为止

Oneway模式：客户端调用完继续执行，不管接收端是否成功。

Reliable模式：为保证通信可靠，将借助于消息中心来实现消息的可靠送达，请求将做持久化存储，在接收方在线时做送达，并由消息中心保证异常重试。

 

 

 

 

 

 

=======================================================================Hessian与Webservice的区别=======================================================================

Hessian:hessian是一个轻量级的remoting onhttp工具，使用简单的方法提供了RMI的功能，相比WebService，Hessian更简单、快捷。

采用的是二进制RPC协议，因为采用了二进制协议，所以它很适合于发送二进制数据，Hessian主要作面向对象的消息通信。

Hessian：写一个Hessian需要注意的问题：      

1、JAVA服务器端必须具备以下几点：        

包含Hessian的jar包          

设计一个接口，用来给客户端调用        

实现该接口的动能          

配置web.xml,配置相应的servlet        

对象必须实现Serializable接口          

对于复杂对象可以使用Map的方法传递    

2、客户端必须具备以下几点：        

java客户端包含Hessian.jar包          

具有和服务器端结构一样的接口和实体类。包括命名空间都最好一样。

 

Hessian的优点：

1- 整个jar很小,200多K,3.1版本的,当然,我下载的for java的版本.

2- 配置很简单,基本上不需要花什么经历就配置出来了

3- 功能强大,可以将soap抛开,也可以把EJB抛开,采用二进制来传递对象

4- 拥有多种语言支持,Python c++  .net 甚至 flex 都可以做为client端

 

 

=======================================================================Java 性能调优的 11 个实用技巧=======================================================================

尽可能使用基本数据类型：

另一种避免开销，提高应用程序性能的快速方法就是使用原始数据类型而不是它们的包装类。因此，最好是使用int而不是Integer，或者是double而不是Double。这将让JVM将值存储在堆栈中，以减少内存消耗，并更有效地处理它。

 

尽量避免BigInteger和BigDecimal

由于我们已经讨论了数据类型，我们再来看下BigInteger和BigDecimal。尤其是后者，由于其精度高而受欢迎。但这是有代价的。

BigInteger和BigDecimal比简单的long或double需要更多的内存，并且大大降低所有的计算速度。因此，如果你需要额外的精度，或者你的数字超过了一个long范围，最好三思而后行。这可能是你在提升性能问题中唯一需要更改的地方，特别是当你正在实现一个数学算法。

 

使用Apache Commons StringUtils.Replace 代替String.replace

一般来说,String.replace 方法工作得很好，而且非常高效，特别是如果你使用的是Java 9。但是，如果应用程序需要大量的替换操作，并且你还没有更新到最新的Java版本，那么检查更快和更有效的替代方案仍然是有意义的。

一个候选就是 Apache Commons Lang’s StringUtils.replace 方法。正如Lukas Eder在他最近的一篇博客文章中所描述的那样，它大大超过了Java 8的String.replace 方法。

 

 

 

！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！

如果能估计到待添加的内容长度，为底层以数组方式实现的集合、工具类指定初始长度

比如ArrayList、LinkedLlist、StringBuilder、StringBuffer、HashMap、HashSet等等，以StringBuilder为例：

StringBuilder()　　　　　　// 默认分配16个字符的空间

StringBuilder(int size)　　// 默认分配size个字符的空间

StringBuilder(String str)　// 默认分配16个字符+str.length()个字符空间

可以通过类（这里指的不仅仅是上面的StringBuilder）的构造函数来设定它的初始化容量，这样可以明显地提升性能。比如StringBuilder吧，length表示当前的StringBuilder能保持的字符数量。因为当StringBuilder达到最大容量的时候，它会将自身容量增加到当前的2倍再加2，无论何时只要StringBuilder达到它的最大容量，它就不得不创建一个新的字符数组然后将旧的字符数组内容拷贝到新字符数组中—-这是十分耗费性能的一个操作。试想，如果能预估到字符数组中大概要存放5000个字符而不指定长度，最接近5000的2次幂是4096，每次扩容加的2不管，那么：

 

在4096 的基础上，再申请8194个大小的字符数组，加起来相当于一次申请了12290个大小的字符数组，如果一开始能指定5000个大小的字符数组，就节省了一倍以上的空间

把原来的4096个字符拷贝到新的的字符数组中去

这样，既浪费内存空间又降低代码运行效率。所以，给底层以数组实现的集合、工具类设置一个合理的初始化容量是错不了的，这会带来立竿见影的效果。但是，注意，像HashMap这种是以数组+链表实现的集合，别把初始大小和你估计的大小设置得一样，因为一个table上只连接一个对象的可能性几乎为0。初始大小建议设置为2的N次幂，如果能估计到有2000个元素，设置成new HashMap(128)、new HashMap(256)都可以。

 

 

当复制大量数据时，使用System.arraycopy()命令

 

 

乘法和除法使用移位操作

 

例如：

for (val = 0; val < 100000; val += 5)

{

　　a = val * 8;

　　b = val / 2;

}

用移位操作可以极大地提高性能，因为在计算机底层，对位的操作是最方便、最快的，因此建议修改为：

 

 

for (val = 0; val < 100000; val += 5)

{

　　a = val << 3;

　　b = val >> 1;

}

移位操作虽然快，但是可能会使代码不太好理解，因此最好加上相应的注释。

 

 

 

循环内不要不断创建对象引用：

例如：

for (int i = 1; i <= count; i++)

{

​    Object obj = new Object();    

}

这种做法会导致内存中有count份Object对象引用存在，count很大的话，就耗费内存了，建议为改为：

 

Object obj = null;

for (int i = 0; i <= count; i++)

{

​    obj = new Object();

}

这样的话，内存中只有一份Object对象引用，每次new Object()的时候，Object对象引用指向不同的Object罢了，但是内存中只有一份，这样就大大节省了内存空间了。

 

 

！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！

基于效率和类型检查的考虑，应该尽可能使用array，无法确定数组大小时才使用ArrayList

 

 

尽量使用HashMap、ArrayList、StringBuilder，除非线程安全需要，否则不推荐使用Hashtable、Vector、StringBuffer，后三者由于使用同步机制而导致了性能开销

 

不要将数组声明为public static final

因为这毫无意义，这样只是定义了引用为static final，数组的内容还是可以随意改变的，将数组声明为public更是一个安全漏洞，这意味着这个数组可以被外部类所改变

 

 

尽量在合适的场合使用单例

使用单例可以减轻加载的负担、缩短加载的时间、提高加载的效率，但并不是所有地方都适用于单例，简单来说，单例主要适用于以下三个方面：

控制资源的使用，通过线程同步来控制资源的并发访问

控制实例的产生，以达到节约资源的目的

控制数据的共享，在不建立直接关联的条件下，让多个不相关的进程或线程之间实现通信

 

 

尽量避免随意使用静态变量

要知道，当某个对象被定义为static的变量所引用，那么gc通常是不会回收这个对象所占有的堆内存的，如：

public class A

{

​    private static B b = new B();  

}

此时静态变量b的生命周期与A类相同，如果A类不被卸载，那么引用B指向的B对象会常驻内存，直到程序终止

 

 

将常量声明为static final，并以大写命名

这样在编译期间就可以把这些内容放入常量池中，避免运行期间计算生成常量的值。另外，将常量的名字以大写命名也可以方便区分出常量与变量

 

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!    

程序运行过程中避免使用反射

反射是Java提供给用户一个很强大的功能，功能强大往往意味着效率不高。不建议在程序运行过程中使用尤其是频繁使用反射机制，特别是Method的invoke方法，如果确实有必要，

一种建议性的做法是将那些需要通过反射加载的类在项目启动的时候通过反射实例化出一个对象并放入内存—-用户只关心和对端交互的时候获取最快的响应速度，并不关心对端的项目启动花多久时间。    

​    

 

使用数据库连接池和线程池

这两个池都是用于重用对象的，前者可以避免频繁地打开和关闭连接，后者可以避免频繁地创建和销毁线程    

​    

 

使用带缓冲的输入输出流进行IO操作

带缓冲的输入输出流，即BufferedReader、BufferedWriter、BufferedInputStream、BufferedOutputStream，这可以极大地提升IO效率

 

顺序插入和随机访问比较多的场景使用ArrayList，元素删除和中间插入比较多的场景使用LinkedList

 

把一个基本数据类型转为字符串，基本数据类型.toString()是最快的方式、String.valueOf(数据)次之、数据+”"最慢

 

对资源的close()建议分开操作,XXX.close()抛异常了，那么就进入了catch块中了，YYY.close()不会执行，YYY这块资源就不会回收了，一直占用着

 

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

对于ThreadLocal使用前或者使用后一定要先remove

 

当前基本所有的项目都使用了线程池技术，这非常好，可以动态配置线程数、可以重用线程。

 

然而，如果你在项目中使用到了ThreadLocal，一定要记得使用前或者使用后remove一下。这是因为上面提到了线程池技术做的是一个线程重用，这意味着代码运行过程中，一条线程使用完毕，并不会被销毁而是等待下一次的使用。我们看一下Thread类中，持有ThreadLocal.ThreadLocalMap的引用：

 

ThreadLocal.ThreadLocalMap threadLocals = null;

线程不销毁意味着上条线程set的ThreadLocal.ThreadLocalMap中的数据依然存在，那么在下一条线程重用这个Thread的时候，很可能get到的是上条线程set的数据而不是自己想要的内容。

 

这个问题非常隐晦，一旦出现这个原因导致的错误，没有相关经验或者没有扎实的基础非常难发现这个问题，因此在写代码的时候就要注意这一点，这将给你后续减少很多的工作量。

 

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

避免Random实例被多线程使用，虽然共享该实例是线程安全的，但会因竞争同一seed 导致的性能下降，JDK7之后，可以使用ThreadLocalRandom来获取随机数,多个线程同时获取随机数的时候，会竞争同一个seed，导致了效率的降低。

 

 

进行适当的锁分解,考虑下面这段程序：

public class GameServer {

  public Map<String, List<Player>> tables = new HashMap<String, List<Player>>();

  public void join(Player player, Table table) {

​    if (player.getAccountBalance() > table.getLimit()) {

​      synchronized (tables) {

​        List<Player> tablePlayers = tables.get(table.getId());

​        if (tablePlayers.size() < 9) {

​          tablePlayers.add(player);

​        }

​      }

​    }

  }

  public void leave(Player player, Table table) {/*省略*/}

  public void createTable() {/*省略*/}

  public void destroyTable(Table table) {/*省略*/}

}

在这个例子中，join方法只使用一个同步锁，来获取tables中的List<Player>对象，然后判断玩家数量是不是小于9，如果是，就调增加一个玩家。当有成千上万个List<Player>存在tables中时，对tables锁的竞争将非常激烈。在这里，我们可以考虑进行锁的分解：快速取出数据之后，对List<Player>对象进行加锁，让其他线程可快速竞争获得tables对象锁：

public class GameServer {

  public Map<String, List<Player>> tables = new HashMap<String, List<Player>>();

  public void join(Player player, Table table) {

​    if (player.getAccountBalance() > table.getLimit()) {

​      List<Player> tablePlayers = null;

​      synchronized (tables) {

​          tablePlayers = tables.get(table.getId());

​      }

​       

​      synchronized (tablePlayers) {

​        if (tablePlayers.size() < 9) {

​          tablePlayers.add(player);

​        }

​      }

​    }

  }

public void leave(Player player, Table table) {/*省略*/}

public void createTable() {/*省略*/}

public void destroyTable(Table table) {/*省略*/}

}

=======================================================================反射的作用=======================================================================

Java反射描述的是，在运行状态中：

1、对于任意一个类，都能够知道这个类的所有属性和方法

2、对于任意一个类，都能够调用它的任意一个属性和方法

之所以强调属性、方法，是因为属性、方法是开发者对于一个类最关注的两个部分。实际上通过反射，不仅仅可以获知类的属性、方法，还可以获知类的父类、接口、包等信息

​    

一个类在加载的时候，会在内存中生成一个代表这个.class文件的java.lang.Class对象，.classs文件里面就包含了描述这个类的信息的一切内容。    

​    

​    

​    

=======================================================================并发队列 ConcurrentLinkedQueue=======================================================================    

ConcurrentLinkedQueue不支持阻塞，没有BlockingQueue那么易用；但在中等规模的并发场景下，其性能却比BlockingQueue高不少，而且相当稳定。    

Java提供的线程安全的Queue可以分为阻塞队列和非阻塞队列，其中阻塞队列的典型例子是BlockingQueue，非阻塞队列的典型例子是ConcurrentLinkedQueue

线程安全就是说多线程访问同一代码，不会产生不确定的结果。

 

并行和并发区别

1、并行是指两者同时执行一件事，比如赛跑，两个人都在不停的往前跑；

2、并发是指资源有限的情况下，两者交替轮流使用资源，比如一段路(单核CPU资源)同时只能过一个人，A走一段后，让给B，B用完继续给A ，交替使用，目的是提高效率

 

LinkedBlockingQueue是一个线程安全的阻塞队列，它实现了BlockingQueue接口，BlockingQueue接口继承自java.util.Queue接口，并在这个接口的基础上增加了take和put方法，这两个方法正是队列操作的阻塞版本。

ConcurrentLinkedQueue是Queue的一个安全实现．Queue中元素按FIFO原则进行排序．采用CAS操作，来保证元素的一致性。

 

 

ConcurrentLinkedQueue的API原来.size()是要遍历一遍集合的，难怪那么慢，所以尽量要避免用size而改用isEmpty().

 

 

public class ConcurrentLinkedQueueTest {

​    private static ConcurrentLinkedQueue<Integer> queue = new ConcurrentLinkedQueue<Integer>();

​    private static int count = 2; // 线程个数

​    //CountDownLatch，一个同步辅助类，在完成一组正在其他线程中执行的操作之前，它允许一个或多个线程一直等待。

​    private static CountDownLatch latch = new CountDownLatch(count);

 

​    public static void main(String[] args) throws InterruptedException {

​        long timeStart = System.currentTimeMillis();

​        ExecutorService es = Executors.newFixedThreadPool(4);

​        ConcurrentLinkedQueueTest.offer();

​        for (int i = 0; i < count; i++) {

​            es.submit(new Poll());

​        }

​        latch.await(); //使得主线程(main)阻塞直到latch.countDown()为零才继续执行

​        System.out.println("cost time " + (System.currentTimeMillis() - timeStart) + "ms");

​        es.shutdown();

​    }

​    

​    /**

​     \* 生产

​     */

​    public static void offer() {

​        for (int i = 0; i < 100000; i++) {

​            queue.offer(i);

​        }

​    }

 

​    /**

​     \* 消费

​     \*  

​     \* @author 林计钦

​     \* @version 1.0 2013-7-25 下午05:32:56

​     */

​    static class Poll implements Runnable {

​        public void run() {

​            // while (queue.size()>0) {

​            while (!queue.isEmpty()) {    //queue.isEmpty()   Volatile标记，所以也是线程安全的。

​                System.out.println(queue.poll());

​            }

​            latch.countDown();

​        }

​    }

}

 

ConcurrentXXX  的线程安全 体现在：  多个线程在同时操作 ConcurrentXXX 的 put  take  不会出现线程安全问题,而不是多个线程同时操作ConcurrentXXX这个对象。

=======================================================================IO=======================================================================    

以文件IO为例,一个IO读过程是文件数据从磁盘→内核缓冲区→用户内存的过程。同步与异步的区别主要在于数据从内核缓冲区→用户内存这个过程需不需要用户进程等待。

BIO就是指IO，即传统的Blocking IO,即同步并阻塞的IO。依赖于ServerSocket实现，即一个请求对应一个线程，如果线程数不够连接则会等待空余线程或者拒绝连接。

在高并发情况下效率是很低的，也不可靠，一般只应用于连接数比较小且固定架构的应用，但api也比较容易使用。

NIO,新的IO,即New IO或者Non-Blocking IO,即同步不阻塞的IO

相比于传统的BIO,NIO 提供了高速的面向快的I/O,它加入了Buffer、Channel、Selector等概念。

它是基于事件驱动的，采用了Reactor模式，它使用一个线程管理所有的socket通道，即客户端发送的连接请求都会注册到多路复用器上，多路复用器轮询到连接有I/O请求时才启动一个线程进行处理。它的特点是要不断主动地去询问数据有没有处理完，一般只适用于连接数目较大但连接时间短的应用，如聊天应用等。

AIO

新的IO2.0，即NIO2.0，jdk1.7开始应用，叫做异步不阻塞的IO。AIO引入异常通道的概念，采用了Proactor模式，

一个有效的请求才启动一个线程，它的特点是先由操作系统完成后才通知服务端程序启动线程去处理，一般适用于连接数较多且连接时间长的应用。

BIO 读和写都阻塞操作,读到流或者写流入操作系统才会关流,

 

reactor :负责对IO的响应,不管结果,有问必答。负责观察

proactor:派发,异步操作,不关注结果,由操作系统完成读或者写。可以拿异步消息来理解.

 

BIO:人去饭店吃饭,一直等着,啥也干不了

NIO:打电话给饭店,我要吃排骨。服务员说:好的,然后我去干其他事了,过了半个小时,我又打电话问,好了吗。又回答:还在做。不必等着 ,可以做其他事,有问必答

AIO:在美团上下单,点了酸菜鱼,过了半个销售,服务员打电话给你,到你家门口了,来取。

 

应用场景：并发连接数不多时采用BIO，因为它编程和调试都非常简单，但如果涉及到高并发的情况，应选择NIO或AIO，更好的建议是采用成熟的网络通信框架Netty。

 

 

创建一个新文件：

File f=new File("D:\\hello.txt");     =====》  String fileName="D:"+File.separator+"hello.txt";

f.createNewFile();

 

File类的两个常量：

System.out.println(File.separator);

System.out.println(File.pathSeparator);

\

;

直接在windows下使用\进行分割不行吗？当然是可以的。但是在linux下就不是\了。所以，要想使得我们的代码跨平台，更加健壮

 

删除一个文件：

if(f.exists()){

​    f.delete();

}

 

创建一个文件夹：

String fileName="D:"+File.separator+"hello";

File f=new File(fileName);

f.mkdir();

列出指定目录的全部文件（包括隐藏文件）：

String fileName="D:"+File.separator;

File f=new File(fileName);

File[] str=f.listFiles();

 

判断一个指定的路径是否为目录：

 File f=new File(fileName);

 if(f.isDirectory()){}

 

向文件中追加新内容：

OutputStream out =new FileOutputStream(f,true);

 

法2：

public static void writeFile(String filePath, String content) {

​    // 判断文件路径是否为空

​    if (null == filePath || "".equals(filePath.trim())) {

​        throw new IllegalArgumentException("file path is null!");

​    }

 

​    // 截取路径最后一位"\"或"/"

​    filePath = filePath.trim();

​    String lastChar = filePath.substring(filePath.length() - 1, filePath.length());

​    if ("\\".equals(lastChar) || "/".equals(lastChar)) {

​        filePath = filePath.substring(0, filePath.length() - 1);

​    }

 

​    RandomAccessFile randomFile = null;

​    try {

​        randomFile = new RandomAccessFile(filePath, "rw");

 

​        // 文件长度，字节数

​        long fileLength = randomFile.length();

 

​        // 将写文件指针移到文件尾。

​        randomFile.seek(fileLength);

 

​        randomFile.write(content.getBytes("gbk"));

​    } catch (FileNotFoundException e) {

​        logger.error("", e);

​    } catch (IOException e) {

​        logger.error("", e);

​    } finally {

​        if (null != randomFile) {

​            try {

​                randomFile.close();

​            } catch (IOException e) {

​                logger.error("", e);

​            }

​        }

​    }

}

​    

​    

这样节省空间：

File f=new File(fileName);

InputStream in=new FileInputStream(f);

byte[] b=new byte[(int)f.length()];

in.read(b);

我们不知道文件有多大：

InputStream in=new FileInputStream(f);

 byte[] b=new byte[1024];

 int count =0;

 int temp=0;

 while((temp=in.read())!=(-1)){

 b[count++]=(byte)temp;

 }

 

实际上字节流在操作的时候本身是不会用到缓冲区的，是文件本身的直接操作的，但是字符流在操作的 时候下后是会用到缓冲区的，是通过缓冲区来操作文件的。

使用字节流好还是字符流好呢？

答案是字节流。首先因为硬盘上的所有文件都是以字节的形式进行传输或者保存的，包括图片等内容。但是字符只是在内存中才会形成的，所以在开发中，字节流使用广泛。

 

 

管道流主要可以进行两个线程之间的通信。

PipedOutputStream 管道输出流

PipedInputStream 管道输入流

=======================================================================NIO=======================================================================    

https://mp.weixin.qq.com/s/c9tkrokcDQR375kiwCeV9w?

 

阻塞方式下读取或者写入函数将一直等待，而非阻塞方式下，读取或者写入函数会立即返回一个状态值

 

JavaIO面向流意味着每次从流中读一个或多个字节，直至读取所有字节，它们没有被缓存在任何地方。此外，它不能前后移动流中的数据。如果需要前后移动从流中读取的数据，需要先将它缓存到一个缓冲区。

NIO的缓冲导向方法略有不同。数据读取到一个它稍后处理的缓冲区，需要时可在缓冲区中前后移动。这就增加了处理过程中的灵活性。

 

IO的各种流是阻塞的。这意味着，当一个线程调用read() 或 write()时，该线程被阻塞，直到有一些数据被读取，或数据完全写入。该线程在此期间不能再干任何事情了。

NIO的非阻塞模式，使一个线程从某通道发送请求读取数据，但是它仅能得到目前可用的数据，如果目前没有数据可用时，就什么都不会获取。而不是保持线程阻塞，所以直至数据变得可以读取之前，该线程可以继续做其他的事情。 非阻塞写也是如此。一个线程请求写入一些数据到某通道，但不需要等待它完全写入，这个线程同时可以去做别的事情。 线程通常将非阻塞IO的空闲时间用于在其它通道上执行IO操作，所以一个单独的线程现在可以管理多个输入和输出通道（channel）。

 

Channel是双向的，既可以用来进行读操作，又可以用来进行写操作。

 

 

 

NIO主要有三大核心部分：Channel(通道)，Buffer(缓冲区), Selector。传统IO基于字节流和字符流进行操作，而NIO基于Channel和Buffer(缓冲区)进行操作，数据总是从通道读取到缓冲区中，或者从缓冲区写入到通道中。

Selector(选择区)用于监听多个通道的事件（比如：连接打开，数据到达）。因此，单个线程可以监听多个数据通道。

NIO和传统IO（一下简称IO）之间第一个最大的区别是，IO是面向流的，NIO是面向缓冲区的。 Java IO面向流意味着每次从流中读一个或多个字节，直至读取所有字节，它们没有被缓存在任何地方。此外，它不能前后移动流中的数据。如果需要前后移动从流中读取的数据，需要先将它缓存到一个缓冲区。

NIO的缓冲导向方法略有不同。数据读取到一个它稍后处理的缓冲区，需要时可在缓冲区中前后移动。这就增加了处理过程中的灵活性。但是，还需要检查是否该缓冲区中包含所有您需要处理的数据。而且，需确保当更多的数据读入缓冲区时，不要覆盖缓冲区里尚未处理的数据。

IO的各种流是阻塞的。这意味着，当一个线程调用read() 或 write()时，该线程被阻塞，直到有一些数据被读取，或数据完全写入。该线程在此期间不能再干任何事情了。

Channel：

只不过Stream是单向的，譬如：InputStream, OutputStream.而Channel是双向的，既可以用来进行读操作，又可以用来进行写操作。

NIO中的Channel的主要实现有：

FileChannel

DatagramChannel

SocketChannel

ServerSocketChannel

 

NIO中的关键Buffer实现有：ByteBuffer, CharBuffer, DoubleBuffer, FloatBuffer, IntBuffer, LongBuffer, ShortBuffer，分别对应基本数据类型: byte, char, double, float, int, long, short。当然NIO中还有MappedByteBuffer, HeapByteBuffer, DirectByteBuffer等这里先不进行陈述。

 

 

使用Buffer一般遵循下面几个步骤：

分配空间（ByteBuffer buf = ByteBuffer.allocate(1024); 还有一种allocateDirector后面再陈述）

写入数据到Buffer(int bytesRead = fileChannel.read(buf);)

调用filp()方法（ buf.flip();）   //读写转换

从Buffer中读取数据（System.out.print((char)buf.get());）

调用clear()方法或者compact()方法

 

filp() : 该操作会重置position，通常，将buffer从写模式转换为读 模式时需要执行此方法 flip()操作不仅重置了当前的position为0，还将limit设置到当前position的位置 。

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

向Buffer中写数据：

从Channel写到Buffer (fileChannel.read(buf))

通过Buffer的put()方法 （buf.put(…)）

从Buffer中读取数据：

从Buffer读取到Channel (channel.write(buf))

使用get()方法从Buffer中读取数据 （buf.get()）

public static void method1(){

​       RandomAccessFile aFile = null;

​       try{

​           aFile = new RandomAccessFile("src/nio.txt","rw");

​           FileChannel fileChannel = aFile.getChannel();

​           ByteBuffer buf = ByteBuffer.allocate(1024);

​           int bytesRead = fileChannel.read(buf);

​           System.out.println(bytesRead);

​           while(bytesRead != -1)

​           {

​               buf.flip();

​               while(buf.hasRemaining())

​               {

​                   System.out.print((char)buf.get());

​               }

​               buf.compact();

​               bytesRead = fileChannel.read(buf);

​           }

​       }catch (IOException e){

​           e.printStackTrace();

​       }finally{

​           try{

​               if(aFile != null){

​                   aFile.close();

​               }

​           }catch (IOException e){

​               e.printStackTrace();

​           }

​       }

}

 

 

 

使用NIO来复制文件：

public static void nioCopyFile(String resource, String destination)

​            throws IOException {

​        FileInputStream fis = new FileInputStream(resource);

​        FileOutputStream fos = new FileOutputStream(destination);

​        FileChannel readChannel = fis.getChannel(); // 读文件通道

​        FileChannel writeChannel = fos.getChannel(); // 写文件通道

​        ByteBuffer buffer = ByteBuffer.allocate(1024); // 读入数据缓存

​        while (true) {

​            buffer.clear();

​            int len = readChannel.read(buffer); // 读入数据

​            if (len == -1) {

​                break; // 读取完毕

​            }

​            buffer.flip();

​            writeChannel.write(buffer); // 写入文件

​        }

​        readChannel.close();

​        writeChannel.close();

}

 

 

NIO有一个很大的特点就是：把数据准备好了再通知我

而Channel有点类似于流，一个Channel可以和文件或者网络Socket对应 。

多线程网络服务器的一般结构：、

 

 

客户端-----              --------------Socket----------线程

​          |              |

​          |              |

客户端--------------派发 --------------Socket----------线程

​          |              |

​          |              |

客户端-----               --------------Socket----------线程

​                

​                

 

NIO:

​                --------------Channel------Socket

​                |

​                |

线程----selector--------------Channel------Socket

​                |

​                |

​                --------------Channel------Socket

 

 

selector是一个选择器，它可以选择某一个Channel，然后做些事情。

一个线程可以对应一个selector，而一个selector可以轮询多个Channel，而每个Channel对应了一个Socket。

与上面一个线程对应一个Socket相比，使用NIO后，一个线程可以轮询多个Socket。

 

！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！

当selector调用select()时，会查看是否有客户端准备好了数据。当没有数据被准备好时，select()会阻塞。平时都说NIO是非阻塞的，但是如果没有数据被准备好还是会有阻塞现象。

当有数据被准备好时，调用完select()后，会返回一个SelectionKey，SelectionKey表示在某个selector上的某个Channel的数据已经被准备好了。

只有在数据准备好时，这个Channel才会被选择。

这样NIO实现了一个线程来监控多个客户端。

某个Socket网络延迟时，数据还未被准备好，selector是不会选择它的，而会选择其他准备好的客户端。

selectNow()与select()的区别在于，selectNow()是不阻塞的，当没有客户端准备好数据时，selectNow()不会阻塞，将返回0，有客户端准备好数据时，selectNow()返回准备好的客户端的个数。

 

 

原来的 I/O 库(在 java.io.*中) 与 NIO 最重要的区别是数据打包和传输的方式。正如前面提到的，原来的 I/O 以流的方式处理数据，而 NIO 以块的方式处理数据。

面向流 的 I/O 系统一次一个字节地处理数据。

 

通道 和 缓冲区 是 NIO 中的核心对象，通道是对原 I/O 包中的流的模拟。到任何目的地(或来自任何地方)的所有数据都必须通过一个 Channel 对象。一个 Buffer 实质上是一个容器对象。发送给一个通道的所有对象都必须首先放到缓冲区中；同样地，从通道中读取的任何数据都要读到缓冲区中。

 

Buffer（缓冲区） 是一个对象， 它包含一些要写入或者刚读出的数据。 在 NIO 中加入 Buffer 对象，体现了新库与原 I/O 的一个重要区别。在面向流的 I/O 中，您将数据直接写入或者将数据直接读到 Stream 对象中。

在 NIO 库中，所有数据都是用缓冲区处理的。在读取数据时，它是直接读到缓冲区中的。在写入数据时，它是写入到缓冲区中的。任何时候访问 NIO 中的数据，您都是将它放到缓冲区中。

缓冲区实质上是一个数组。通常它是一个字节数组，但是也可以使用其他种类的数组。但是一个缓冲区不 仅仅 是一个数组。缓冲区提供了对数据的结构化访问，而且还可以跟踪系统的读/写进程。

最常用的缓冲区类型是 ByteBuffer。

 

Channel是一个对象，可以通过它读取和写入数据。拿 NIO 与原来的 I/O 做个比较，通道就像是流。

所有数据都通过Buffer对象来处理。您永远不会将字节直接写入通道中，相反，您是将数据写入包含一个或者多个字节的缓冲区。同样，您不会直接从通道中读取字节，而是将数据从通道读入缓冲区，再从缓冲区获取这个字节。

 

通道与流的不同之处在于通道是双向的。而流只是在一个方向上移动(一个流必须是 InputStream 或者 OutputStream 的子类)， 而 通道 可以用于读、写或者同时用于读写。

 

从一个通道中读取很简单：只需创建一个缓冲区，然后让通道将数据读到这个缓冲区中。写入也相当简单：创建一个缓冲区，用数据填充它，然后让通道用这些数据来执行写入操作。

在 NIO 系统中，任何时候执行一个读操作，您都是从通道中读取，但是您不是 直接 从通道读取。因为所有数据最终都驻留在缓冲区中，所以您是从通道读到缓冲区中。

 

 

读取文件：

第一步是获取通道。我们从 FileInputStream 获取通道：

FileInputStream fin = new FileInputStream( "readandshow.txt" );

FileChannel fc = fin.getChannel();

下一步是创建缓冲区：

ByteBuffer buffer = ByteBuffer.allocate( 1024 );

最后，需要将数据从通道读到缓冲区中，如下所示：

fc.read(buffer);

 

 

写入文件：

在 NIO 中写入文件类似于从文件中读取。首先从 FileOutputStream 获取一个通道：

FileOutputStream fout = new FileOutputStream( "writesomebytes.txt" );

FileChannel fc = fout.getChannel();

下一步是创建一个缓冲区并在其中放入一些数据 – 在这里，数据将从一个名为 message 的数组中取出，这个数组包含字符串 “Some bytes” 的 ASCII 字节

ByteBuffer buffer = ByteBuffer.allocate( 1024 );

for (int i=0; i<message.length; ++i) {

buffer.put( message[i] );

}

buffer.flip();

最后一步是写入缓冲区中

fc.write( buffer );

 

 

ByteBuffer 类中有四个 get() 方法：

byte get();

ByteBuffer get( byte dst[] );

ByteBuffer get( byte dst[], int offset, int length );

byte get( int index );

第一个方法获取单个字节。第二和第三个方法将一组字节读到一个数组中。第四个方法从缓冲区中的特定位置获取字节。

 

ByteBuffer 类中有五个 put() 方法：

ByteBuffer put( byte b );

ByteBuffer put( byte src[] );

ByteBuffer put( byte src[], int offset, int length );

ByteBuffer put( ByteBuffer src );

ByteBuffer put( int index, byte b );

 

 

下面的内部循环概括了使用缓冲区将数据从输入通道拷贝到输出通道的过程：

while (true) {

buffer.clear();

int r = fcin.read( buffer );

if (r==-1) {

break;

}

buffer.flip();

fcout.write( buffer );

}

read() 和 write() 调用得到了极大的简化，因为许多工作细节都由缓冲区完成了。 clear() 和 flip() 方法用于让缓冲区在读和写之间切换。

 

！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！内存映射文件 I/O ！！！！！！！！！！！！！！！！！

内存映射文件 I/O：

内存映射文件 I/O 是一种读和写文件数据的方法，！！！！！！它可以比常规的基于流或者基于通道的 I/O 快得多。！！！！！

是通过使文件中的数据神奇般地出现为内存数组的内容来完成的。这起初听起来似乎不过就是将整个文件读到内存中，但是事实上并不是这样。一般来说，只有文件中实际读取或者写入的部分才会送入（或者 映射 ）到内存中。

 

尽管创建内存映射文件相当简单，但是向它写入可能是危险的。仅只是改变数组的单个元素这样的简单操作，就可能会直接修改磁盘上的文件。修改数据与将数据保存到磁盘是没有分开的。

 

 

文件映射到内存:

public static void main(String[] args) throws Exception {

​        RandomAccessFile raf = new RandomAccessFile("C:\\mapfile.txt", "rw");

​        FileChannel fc = raf.getChannel();

​        // 将文件映射到内存中

​        MappedByteBuffer mbb = fc.map(FileChannel.MapMode.READ_WRITE, 0,

​                raf.length());

​        while (mbb.hasRemaining()) {

​            System.out.print((char) mbb.get());

​        }

​        mbb.put(0, (byte) 98); // 修改文件

​        raf.close();

}

对MappedByteBuffer的修改就相当于修改文件本身，这样操作的速度是很快的。

map() 方法返回一个 MappedByteBuffer，它是 ByteBuffer 的子类。因此，您可以像使用其他任何 ByteBuffer 一样使用新映射的缓冲区，操作系统会在需要时负责执行行映射。

 

 

 

在 NIO 中执行简单的文件锁过程

RandomAccessFile raf = new RandomAccessFile( "usefilelocks.txt", "rw" );

FileChannel fc = raf.getChannel();

FileLock lock = fc.lock( start, end, false );

在拥有锁之后，您可以执行需要的任何敏感操作，然后再释放锁：

lock.release();

 

 

Selector(选择区)用于监听多个通道的事件（比如：连接打开，数据到达）。因此，单个线程可以监听多个数据通道。

 

 

！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！

NIO中的Channel的主要实现有：  分别可以对应文件IO、UDP和TCP

FileChannel

DatagramChannel

SocketChannel

ServerSocketChannel

 

=======================================================================AIO=======================================================================    

AIO的特点：    有点像异步ajax

\1. 读完了再通知我

\2. 不会加快IO，只是在读完后进行通知

\3. 使用回调函数，进行业务处理

 

 

jdk7主要增加了三个新的异步通道:

AsynchronousFileChannel: 用于文件异步读写；

AsynchronousSocketChannel: 客户端异步socket；

AsynchronousServerSocketChannel: 服务器异步socket。

 

AIO的相关代码：

AsynchronousServerSocketChannel

server = AsynchronousServerSocketChannel.open().bind( new InetSocketAddress (PORT));

使用server上的accept方法

public abstract <A> void accept(A attachment,CompletionHandler<AsynchronousSocketChannel,? super A> handler);

 

CompletionHandler 为回调接口，当有客户端accept之后，就做handler中的事情。

 

在理解了NIO的基础上，看AIO，区别在于AIO是等读写过程完成后再去调用回调函数。

NIO是同步非阻塞的

AIO是异步非阻塞的

 

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

由于NIO的读写过程依然在应用线程里完成，所以对于那些读写过程时间长的，NIO就不太适合。

而AIO的读写过程完成后才被通知，所以AIO能够胜任那些重量级，读写过程长的任务。

 

（Java AIO(NIO.2)）异步非阻塞IO:  

在此种模式下，用户进程只需要发起一个IO操作然后立即返回，等IO操作真正的完成以后，应用程序会得到IO操作完成的通知，此时用户进程只需要对数据进行处理就好了，不需要进行实际的IO读写操作，因为真正的IO读取或者写入操作已经由内核完成了。

同步非阻塞IO(Java NIO) ： 同步非阻塞，服务器实现模式为一个请求一个线程，即客户端发送的连接请求都会注册到多路复用器上，多路复用器轮询到连接有I/O请求时才启动一个线程进行处理。用户进程也需要时不时的询问IO操作是否就绪，这就要求用户进程不停的去询问。

 

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

BIO、NIO、AIO适用场景分析:

​    BIO方式适用于连接数目比较小且固定的架构，这种方式对服务器资源要求比较高，并发局限于应用中，JDK1.4以前的唯一选择，但程序直观简单易理解。

​    NIO方式适用于连接数目多且连接比较短（轻操作）的架构，比如聊天服务器，并发局限于应用中，编程比较复杂，JDK1.4开始支持。

​    AIO方式使用于连接数目多且连接比较长（重操作）的架构，比如相册服务器，充分调用OS参与并发操作，编程比较复杂，JDK7开始支持。

​    

如果你想吃一份宫保鸡丁盖饭：

​    同步阻塞：你到饭馆点餐，然后在那等着，还要一边喊：好了没啊！

​    同步非阻塞：在饭馆点完餐，就去遛狗了。不过溜一会儿，就回饭馆喊一声：好了没啊！

​    异步阻塞：遛狗的时候，接到饭馆电话，说饭做好了，让您亲自去拿。

​    异步非阻塞：饭馆打电话说，我们知道您的位置，一会给你送过来，安心遛狗就可以了。

​    

jdk7中新增了一些与文件(网络)I/O相关的一些api。AIO最大的一个特性就是异步能力，这种能力对socket与文件I/O都起作用。

AIO其实是一种在读写操作结束之前允许进行其他操作的I/O处理。

 

因为AIO的实施需充分调用OS参与，IO需要操作系统支持、并发也同样需要操作系统的支持，所以性能方面不同操作系统差异会比较明显。

 

 

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

异步无非是通知系统做一件事情。然后忘掉它，自己做其他事情去了。很多时候系统做完某一件事情后需要一些后续的操作。怎么办？这时候就是告诉异步调用如何做后续处理。通常有两种方式：

将来式: 当你希望主线程发起异步调用，并轮询等待结果的时候使用将来式;

回调式: 常说的异步回调就是它。

将来式用现有的Java.util.concurrent技术声明一个Future,用来保存异步操作的处理结果。通常用Future get()方法（带或不带超时参数）在异步IO操作完成时获取其结果。  !!!!!用来保存异步操作的处理结果  !!!!!!!!!用来保存异步操作的处理结果

 

AsynchronousFileChannel会关联线程池，它的任务是接收IO处理事件，并分发给负责处理通道中IO操作结果的结果处理器。跟通道中发起的IO操作关联的结果处理器确保是由线程池中的某个线程产生。

将来式例子：

 

Path path = Paths.get("/data/code/github/java_practice/src/main/resources/1log4j.properties");

​    AsynchronousFileChannel channel = AsynchronousFileChannel.open(path);

​    ByteBuffer buffer = ByteBuffer.allocate(1024);

​    Future<Integer> future = channel.read(buffer,0);

//        while (!future.isDone()){

//            System.out.println("I'm idle");

//        }

​    Integer readNumber = future.get();

​    buffer.flip();

​    CharBuffer charBuffer = CharBuffer.allocate(1024);

​    CharsetDecoder decoder = Charset.defaultCharset().newDecoder();

​    decoder.decode(buffer,charBuffer,false);

​    charBuffer.flip();

​    String data = new String(charBuffer.array(),0, charBuffer.limit());

​    System.out.println("read number:" + readNumber);

​    System.out.println(data);

​    

 

！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！    

回调式异步读取：

回调式所采用的事件处理技术类似于Swing UI编程采用的机制。基本思想是主线程会派一个侦查员CompletionHandler到独立的线程中执行IO操作。这个侦查员将带着IO的操作的结果返回到主线程中，这个结果会触发它自己的completed或failed方法（要重写这两个方法）。在异步IO活动结束后，接口[java.nio.channels.CompletionHandler](http://java.nio.channels.completionhandler/)会被调用，其中V是结果类型，A是提供结果的附着对象。此时必须已经有了该接口completed（V,A）和failed(V,A)方法的实现，你的程序才能知道异步IO操作成功或失败时该如何处理。

 

​    Path path = Paths.get("/data/code/github/java_practice/src/main/resources/1log4j.properties");

​    AsynchronousFileChannel channel = AsynchronousFileChannel.open(path);

​    ByteBuffer buffer = ByteBuffer.allocate(1024);

​    channel.read(buffer, 0, buffer, new CompletionHandler<Integer, ByteBuffer>() {              //主线程的read操作不会被阻塞

​        @Override

​        public void completed(Integer result, ByteBuffer attachment) {

​            System.out.println(Thread.currentThread().getName() + " read success!");

​        }

​        @Override

​        public void failed(Throwable exc, ByteBuffer attachment) {

​            System.out.println("read error");

​        }

​    });

​    while (true){

​        System.out.println(Thread.currentThread().getName() + " sleep");

​        Thread.sleep(1000);

​    }    

​    

 

异步socket server操作：

final AsynchronousServerSocketChannel channel = AsynchronousServerSocketChannel

​            .open()

​            .bind(new InetSocketAddress("0.0.0.0",8888));

​    channel.accept(null, new CompletionHandler<AsynchronousSocketChannel, Void>() {

​        @Override

​        public void completed(final AsynchronousSocketChannel client, Void attachment) {

​            channel.accept(null, this);

​            ByteBuffer buffer = ByteBuffer.allocate(1024);

​            client.read(buffer, buffer, new CompletionHandler<Integer, ByteBuffer>() {

​                @Override

​                public void completed(Integer result_num, ByteBuffer attachment) {

​                    attachment.flip();

​                    CharBuffer charBuffer = CharBuffer.allocate(1024);

​                    CharsetDecoder decoder = Charset.defaultCharset().newDecoder();

​                    decoder.decode(attachment,charBuffer,false);

​                    charBuffer.flip();

​                    String data = new String(charBuffer.array(),0, charBuffer.limit());

​                    System.out.println("read data:" + data);

​                    try{

​                        client.close();

​                    }catch (Exception e){}

​                }

​                @Override

​                public void failed(Throwable exc, ByteBuffer attachment) {

​                    System.out.println("read error");

​                }

​            });

​        }

​        @Override

​        public void failed(Throwable exc, Void attachment) {

​            System.out.println("accept error");

​        }

​    });

​    while (true){

​        Thread.sleep(1000);

​    }

 

异步socket client操作：

AsynchronousSocketChannel channel = AsynchronousSocketChannel.open();

​    channel.connect(new InetSocketAddress("10.19.49.158",8888)).get();    //10.19.49.158  服务器端IP

​    ByteBuffer buffer = ByteBuffer.wrap("中文,你好".getBytes());

​    Future<Integer> future = channel.write(buffer);

​    future.get();

​    System.out.println("send ok");

 

 

 

=======================================================================将来式=======================================================================

将来式

 

用现有的Java.util.concurrent技术声明一个Future,用来保存异步操作的处理结果。通常用Future get()方法（带或不带超时参数）在异步IO操作完成时获取其结果。

 

Future get()方法  仅在Future.get()会阻塞，其他时候不会阻塞

 

 

 

 

 

 

 

 

 

 

 

 

=======================================================================网络编程=======================================================================    

PC/IP协议是传输层协议，主要解决数据如何在网络中传输，而HTTP是应用层协议，主要解决如何包装数据。Socket，本质上就是一组接口，是对TCP/IP协议的封装和应用(程序员层面上)。

Socket编程主要涉及到客户端和服务器端两个方面，首先是在服务器端创建一个服务器套接字(ServerSocket)，并把它附加到一个端口上，服务器从这个端口监听连接。端口号的范围是0到65536，但是0到1024是为特权服务保留的端口号，我们可以选择任意一个当前没有被其他进程使用的端口。

客户端请求与服务器进行连接的时候，根据服务器的域名或者IP地址，加上端口号，打开一个套接字。当服务器接受连接后，服务器和客户端之间的通信就像输入输出流一样进行操作。

 

为什么传输字节数组 byte[]

这个和主机字节序 网络字节序有关，要和其他非windows系统通信的时候需要。因为byte是字节，已经是传输的最小单位了,计算机处理数据都是按byte来的

在安全性上来讲，转成byte不至于会因为主机序列不同而产生错误。用户可以自己通过对bytes的组合来获取正确的数据。可以这么理解吧

 

 

服务端：

 

public class SocketServer {

​    public static void main(String[] args) throws IOException {

​        // 端口号

​        int port = 7000;

​        // 在端口上创建一个服务器套接字

​        ServerSocket serverSocket = new ServerSocket(port);

​        // 监听来自客户端的连接

​        Socket socket = serverSocket.accept();

 

​        DataInputStream dis = new DataInputStream(

​                new BufferedInputStream(socket.getInputStream()));

​        DataOutputStream dos = new DataOutputStream(

​                new BufferedOutputStream(socket.getOutputStream()));

​        do {

​            double length = dis.readDouble();

​            System.out.println("服务器端收到的边长数据为：" + length);

​            double result = length * length;

​            dos.writeDouble(result);

​            dos.flush();

​        } while (dis.readInt() != 0);

​        socket.close();

​        serverSocket.close();

​    }

}

 

 

客户端：

public class SocketClient {

​    public static void main(String[] args) throws IOException {

 

​        int port = 7000;

 

​        String host = "10.19.49.2";

 

​        // 创建一个套接字并将其连接到指定端口号

​        Socket socket = new Socket(host, port);

 

​        DataInputStream dis = new DataInputStream(new BufferedInputStream(socket.getInputStream()));

 

​        DataOutputStream dos = new DataOutputStream(new BufferedOutputStream(socket.getOutputStream()));

 

​        Scanner sc = new Scanner(System.in);

 

​        boolean flag = false;

 

​        while (!flag) {

 

​            System.out.println("请输入正方形的边长:");

​            double length = sc.nextDouble();

 

​            dos.writeDouble(length);

​            dos.flush();

 

​            double area = dis.readDouble();

 

​            System.out.println("服务器返回的计算面积为:" + area);

 

​            while (true) {

 

​                System.out.println("继续计算？(Y/N)");

 

​                String str = sc.next();

 

​                if (str.equalsIgnoreCase("N")) {

​                    dos.writeInt(0);

​                    dos.flush();

​                    flag = true;

​                    break;

​                } else if (str.equalsIgnoreCase("Y")) {

​                    dos.writeInt(1);

​                    dos.flush();

​                    break;

​                }

​            }

​        }

 

​        socket.close();

​    }

}

 

 

可以看到上面的服务器端程序和客户端程序是一对一的关系，为了能让一个服务器端程序能同时为多个客户提供服务，可以使用多线程机制，每个客户端的请求都由一个独立的线程进行处理。下面是改写后的服务器端程序。

 

public class SocketServerM {

​    public static void main(String[] args) throws IOException {

​        int port = 7000;

​        int clientNo = 1;

​        ServerSocket serverSocket = new ServerSocket(port);

​        // 创建线程池

​        ExecutorService exec = Executors.newCachedThreadPool();

​        try {

​            while (true) {

​                Socket socket = serverSocket.accept();

​                exec.execute(new SingleServer(socket, clientNo));

​                clientNo++;

​            }

​        } finally {

​            serverSocket.close();

​        }

​    }

}

 

class SingleServer implements Runnable {

​    private Socket socket;

​    private int clientNo;

​    public SingleServer(Socket socket, int clientNo) {

​        this.socket = socket;

​        this.clientNo = clientNo;

​    }

​    @Override

​    public void run() {

​        try {

​            DataInputStream dis = new DataInputStream(

​                    new BufferedInputStream(socket.getInputStream()));

​            DataOutputStream dos = new DataOutputStream(

​                    new BufferedOutputStream(socket.getOutputStream()));

​            do {

​                double length = dis.readDouble();

​                System.out.println("从客户端" + clientNo + "接收到的边长数据为：" + length);

​                double result = length * length;

​                dos.writeDouble(result);

​                dos.flush();

​            } while (dis.readInt() != 0);

​        } catch (IOException e) {

​            e.printStackTrace();

​        } finally {

​            System.out.println("与客户端" + clientNo + "通信结束");

​            try {

​                socket.close();

​            } catch (IOException e) {

​                e.printStackTrace();

​            }

​        }

​    }

}

 

 

public Socket accept() throws IOException {

​        if (isClosed())

​            throw new SocketException("Socket is closed");

​        if (!isBound())

​            throw new SocketException("Socket is not bound yet");

​        Socket s = new Socket((SocketImpl) null);

​        implAccept(s);

​        return s;

}

 

上面改进后的服务器端代码可以支持不断地并发响应网络中的客户请求。关键的地方在于多线程机制的运用，同时利用线程池可以改善服务器程序的性能。

 

 

 

 

传字符串：

服务端：

public static void main(String[] args) throws IOException {

​        // 端口号

​        int port = 7000;

​        // 在端口上创建一个服务器套接字

​        ServerSocket serverSocket = new ServerSocket(port);

​        // 监听来自客户端的连接

​        Socket socket = serverSocket.accept();

​        DataInputStream dis = new DataInputStream(

​                new BufferedInputStream(socket.getInputStream()));

​        DataOutputStream dos = new DataOutputStream(

​                new BufferedOutputStream(socket.getOutputStream()));

​        do {

​            byte[] b = new byte[1024];

​            int length = dis.read(b);

​            String c = new String(b,0,length);

​            System.out.println("服务器端收到的边长数据为：" + c);

 

​            String d = c + "again";

​            byte[] b2 = d.getBytes("utf-8");

​            dos.write(b2);

​            dos.flush();

​        } while (dis.readInt() != 0);

​        socket.close();

​        serverSocket.close();

}

 

客户端：

public static void main(String[] args) throws IOException {

​        int port = 7000;

​        String host = "10.19.49.2";

​        // 创建一个套接字并将其连接到指定端口号

​        Socket socket = new Socket(host, port);

​        DataInputStream dis = new DataInputStream(new BufferedInputStream(socket.getInputStream()));

​        DataOutputStream dos = new DataOutputStream(new BufferedOutputStream(socket.getOutputStream()));

​        Scanner sc = new Scanner(System.in);

​        boolean flag = false;

​        while (!flag) {

​            String a = "哈啊啊啊啊啊";

​            byte[] b = a.getBytes("utf-8");

​            dos.write(b);

​            dos.flush();

​            byte[] c = new byte[1024];

​            int i = dis.read(c);

​            String d = new String(c,0,i);

​            System.out.println("服务器返回的计算面积为:" + d);

​            while (true) {

​                System.out.println("继续计算？(Y/N)");

​                String str = sc.next();

​                if (str.equalsIgnoreCase("N")) {

​                    dos.writeInt(0);

​                    dos.flush();

​                    flag = true;

​                    break;

​                } else if (str.equalsIgnoreCase("Y")) {

​                    dos.writeInt(1);

​                    dos.flush();

​                    break;

​                }

​            }

​        }

​        socket.close();

}

 

 

 

NIO实现：

服务器端：  ServerSocketChannel

import java.io.IOException;

import java.net.InetSocketAddress;

import java.nio.ByteBuffer;

import java.nio.channels.ServerSocketChannel;

import java.nio.channels.SocketChannel;

public class Test2 {

​    public static void main(String[] args) throws IOException {

​        ServerSocketChannel ssc = ServerSocketChannel.open();

​        ssc.socket().bind(new InetSocketAddress(8889));

​        String hello_string = "hello rudy!";

​        ByteBuffer buffer = ByteBuffer.wrap(hello_string.getBytes());

​        while (true){

​            SocketChannel clientSocket = ssc.accept();

​            if (null == clientSocket){

​                try {

​                    Thread.sleep(1000);

​                } catch (InterruptedException e) {

​                    e.printStackTrace();

​                }

​            }else{

​                System.out.println(String.format("incomimg connection from: %s",clientSocket.getRemoteAddress()));

​                buffer.rewind();

​                clientSocket.write(buffer);

​                clientSocket.close();

​            }

​        }

​    }

}

 

客户端：    SocketChannel

import java.io.IOException;

import java.net.InetSocketAddress;

import java.nio.ByteBuffer;

import java.nio.CharBuffer;

import java.nio.channels.SocketChannel;

import java.nio.charset.Charset;

import java.nio.charset.CharsetDecoder;

 

public class Test3 {

​    public static void main(String[] args) throws IOException {

​        SocketChannel channel = SocketChannel.open();

​        channel.connect(new InetSocketAddress("服务器IP",8889));

​        ByteBuffer buffer = ByteBuffer.allocate(100);

​        CharBuffer charBuffer = CharBuffer.allocate(100);

​        CharsetDecoder decoder = Charset.defaultCharset().newDecoder();

​        channel.read(buffer);

​        buffer.flip();

​        decoder.decode(buffer,charBuffer,false);

​        charBuffer.flip();

​        while (charBuffer.hasRemaining()){

​            System.out.println(charBuffer.get());

​        }

​        channel.close();

​    }

}

 

 

 

 

 

UDP服务端

​    public static void main(String[] args) throws IOException {

​        DatagramChannel channel = DatagramChannel.open();

​        channel.bind(new InetSocketAddress("localhost",8888));

​        ByteBuffer buffer = ByteBuffer.allocate(100);

​        CharBuffer charBuffer = CharBuffer.allocate(100);

​        CharsetDecoder decoder = Charset.defaultCharset().newDecoder();

​        while (true){

​            buffer.clear();

​            charBuffer.clear();

​            SocketAddress remoteAddress = channel.receive(buffer);

​            buffer.flip();

​            decoder.decode(buffer,charBuffer,false);

​            charBuffer.flip();

​            System.out.println( remoteAddress +":" + new String(charBuffer.array(),0, charBuffer.limit()));

​        }

 

​    }

UDP客户端

​    public static void main(String[] args) throws IOException {

​        DatagramChannel channel = DatagramChannel.open();

​        String sendData = "哈哈哈 hello rudy!";

​        ByteBuffer buffer = ByteBuffer.wrap(sendData.getBytes());

​        channel.send(buffer, new  InetSocketAddress("localhost",8888));

​        System.out.println("send end!");

​    }

 

 

 

 

Selector使用，I/O多路复用：

public static void main(String[] args) throws IOException {

​        Selector selector = Selector.open();

​        ServerSocketChannel channel = ServerSocketChannel.open();

​        channel.bind(new InetSocketAddress("localhost",8888));

​        channel.configureBlocking(false);

 

​        SelectionKey selectionKey = channel.register(selector,SelectionKey.OP_ACCEPT);

 

​        ByteBuffer buffer = ByteBuffer.allocate(1024);

​        CharBuffer charBuffer = CharBuffer.allocate(1024);

​        CharsetDecoder decoder = Charset.defaultCharset().newDecoder();

 

​        while (true){

​            int readyNum = selector.select();

​            if (readyNum <= 0){

​                continue;

​            }

​            Set<SelectionKey> readyKey = selector.selectedKeys();

​            for (SelectionKey tempKey : readyKey){

​                if (tempKey.isAcceptable()){

​                    ServerSocketChannel tempChannel = (ServerSocketChannel) tempKey.channel();

​                    SocketChannel clientChannel = tempChannel.accept();

​                    if (null != clientChannel){

​                        System.out.println("one connection:" + clientChannel.getRemoteAddress());

​                        clientChannel.configureBlocking(false);

​                        clientChannel.register(selector,SelectionKey.OP_READ);

​                    }

​                }

 

​                if(tempKey.isReadable()){

​                    SocketChannel tempChannel = (SocketChannel) tempKey.channel();

​                    tempChannel.read(buffer);

​                    buffer.flip();

​                    decoder.decode(buffer,charBuffer,false);

​                    charBuffer.flip();

​                    String getData = new String(charBuffer.array(),0,charBuffer.limit());

​                    System.out.println(tempChannel.getRemoteAddress() + ":" + getData);

​                    buffer.clear();

​                    charBuffer.clear();

​                    tempChannel.write(ByteBuffer.allocate(0));

​                    if (getData.equalsIgnoreCase("exit")){

​                        tempChannel.close();

​                    }

​                }

 

​                if (tempKey.isWritable()){

​                    SocketChannel tempChannel = (SocketChannel) tempKey.channel();

//                    System.out.println(tempChannel.getRemoteAddress() + ": read");

​                }

​                readyKey.remove(tempKey);

​            }

​        }

​    }

 

 

https://www.jianshu.com/p/a33f741fe450

 

 

http://www.importnew.com/15996.html

 

=======================================================================Netty=======================================================================

官网：

https://netty.io/

 

 

 

 

=======================================================================ModelAndView=======================================================================    

ModelAndView加深理解：

ModelAndView的Model是将它放到request域中，所以只要是在同一个请求中。无论什么时候都能取到它。   只要是在同一个请求中，

如果发了另一个ajax请求，就不是一个请求了,就不能获得上个request请求中的model对象了。

 

但是渲染的问题：

ModelAndView model = new ModelAndView("tianyanNew/ttAging/lineAnalysis");

model.addObject("jzhDistrict", jzhDistrict);

model.addObject("jjjDistrict", jjjDistrict);

return model；

 

Control返回了ModelAndView对象

页面js：

$("#areaLineList").change(function () {

​    let areaLineTemp = $(this).val();

​    if(areaLineTemp == 'jzhRoute'){

​        $('#originProvince').prop("disabled", false);

​        $('#destiProvince').prop("disabled", false);

​        let str=(''+

​                     <#list jzhDistrict as p>

​                    '<option value="${p.code}">${p.name}</option>'+

​                     </#list>'');

​        $("#originProvince").empty();

​        $("#destiProvince").empty();  

​        $("#originProvince").html(str).selectpicker("refresh");

​        $("#destiProvince").html(str).selectpicker("refresh");           

​    }

​    if(areaLineTemp == 'jjjRoute'){

​        $('#originProvince').prop("disabled", false);

​        $('#destiProvince').prop("disabled", false);

​        let str=(''+

​                     <#list jjjDistrict as p>

​                    '<option value="${p.code}">${p.name}</option>'+

​                     </#list>'');

​        $("#originProvince").empty();

​        $("#destiProvince").empty();  

​        $("#originProvince").html(str).selectpicker("refresh");

​        $("#destiProvince").html(str).selectpicker("refresh");           

​    }

}    

页面在渲染的时候：会把 <#list jjjDistrict as p> 这些东西渲染成html页面。 也就是说，如果与上面不是同一个请求了，虽然此时request域中不存在jzhDistrict，jjjDistrict这些对象了，

但是此时页面已经被渲染成了：

$("#areaLineList").change(function () {

​    let areaLineTemp = $(this).val();

​    if(areaLineTemp == 'jzhRoute'){

​        $('#originProvince').prop("disabled", false);

​        $('#destiProvince').prop("disabled", false);

​        let str=(''+

​                    '<option value="010">北京-北京</option>'+

​                                         '<option value="020">广东省-广州市</option>'+

​                                         '<option value="021">上海-上海</option>'+

​                                         '<option value="022">天津-天津</option>');

​        $("#originProvince").empty();

​        $("#destiProvince").empty();  

​        $("#originProvince").html(str).selectpicker("refresh");

​        $("#destiProvince").html(str).selectpicker("refresh");           

​    }

​    if(areaLineTemp == 'jjjRoute'){

​        $('#originProvince').prop("disabled", false);

​        $('#destiProvince').prop("disabled", false);

​        let str=(''+

​                    '<option value="010">重庆-重庆</option>'+

​                                         '<option value="020">辽宁省-辽宁省</option>'+

​                                         '<option value="021">江苏省-江苏省</option>'+

​                                         '<option value="022">西藏-西藏</option>');

​        $("#originProvince").empty();

​        $("#destiProvince").empty();  

​        $("#originProvince").html(str).selectpicker("refresh");

​        $("#destiProvince").html(str).selectpicker("refresh");           

​    }

}    

 

已经不需要从request域中的jzhDistrict，jjjDistrict 取值了。所以即使此时域中没有对象，页面也能有值。

 

 

=======================================================================mysql 字段 is not null 和 字段 !=null=======================================================================

 

注意了  null  不能用 '!='，'='，'<>' 来判断 虽然不会报错，但数据不正确。

应该用，is not null 或 is null

 

 

首先，我们要搞清楚“空值” 和 “NULL” 的概念：

空值是不占用空间的

mysql中的NULL其实是占用空间的

打个比方来说，你有一个杯子，空值代表杯子是真空的，NULL代表杯子中装满了空气，虽然杯子看起来都是空的，但是区别是很大的。

 

测试一下：

CREATE TABLE  `test` (  

`col1` VARCHAR( 10 ) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL ,      //不能插入NULL，但可以是空字符串

`col2` VARCHAR( 10 ) CHARACTER SET utf8 COLLATE utf8_general_ci NULL            //可以插入NULL，和 普通有值的字符串

) ENGINE = MYISAM ;

 

INSERT INTO `test` VALUES (null,1);  

发生错误：   #1048 - Column 'col1' cannot be null

 

INSERT INTO `test` VALUES ('',1);   成功插入。

 

可见，NOT NULL 的字段是不能插入“NULL”的，能插入“空值”

 

为毛not null的效率比null高?

NULL 其实并不是空值，而是要占用空间，所以mysql在进行比较的时候，NULL 会参与字段比较，所以对效率有一部分影响。

而且B树索引时不会存储NULL值的，所以如果索引的字段可以为NULL，索引的效率会下降很多。

 

判断NULL 用IS NULL 或者 IS NOT NULL, SQL语句函数中可以使用ifnull()函数来进行处理，判断空字符用=''或者 <>''来进行处理

对于MySQL特殊的注意事项，对于timestamp数据类型，如果往这个数据类型插入的列插入NULL值，则出现的值是当前系统时间。插入空值，则会出现 0000-00-00 00:00:00

对于空值的判断到底是使用is null 还是='' 要根据实际业务来进行区分。

=======================================================================MYSQL差集 交集 并集=======================================================================

 

差集:

​        SELECT ID FROM (

​             SELECT DISTINCT A.ID AS ID FROM TABLEA A  #有ID： 1 2 3 4 5

​             UNION ALL

​             SELECT DISTINCT B.ID AS ID FROM TABLEB B  #有ID： 2 3

​        )TEMP GROUP BY ID HAVING COUNT(ID) = 1         #合并后分组，找到个数为1的，就是差异的1 4 5

 

Mysql没有提供差集，和交集，

 

为了实现差集和交集，我们可以做合并后，group by

 

COUNT(ID) = 1  差集

COUNT(ID) = 2  交集

 

 

=======================================================================八种排序算法=======================================================================

https://www.cnblogs.com/0201zcr/p/4763806.html

 

http://www.importnew.com/16266.html  

 

平均速度最快：快速排序

​    

排序有内部排序和外部排序，内部排序是数据记录在内存中进行排序，而外部排序是因排序的数据很大，一次不能容纳全部的排序记录，在排序过程中需要访问外存。

我们这里说说八大排序就是内部排序。    

 

 

随机不重复的整数:

我们选择10000个随机不重复整数，可以看出快速排序是最快的，并且是经过多次实验，名副其实，呵呵，它甚至比系统自带的Arrays.sot（）都快

​    

有序不重复整数:

相反我们可以选择一万有个序不重复整数测试，插入排序  的英文最快的，而快速排序就不是最快的了，因为在有序中快速排序效果是很差的但不是最差的。    

​    

​    

冒泡排序算法：可以保证 在值相同的情况下，这个顺序不变

​    Integer a[]=ar.clone();

​    int temp=0;

​    for(int i=0;i<a.length-1;i++){

​        for(int j=0;j<a.length-1-i;j++){

​        if(a[j]>a[j+1]){

​            temp=a[j];

​            a[j]=a[j+1];

​            a[j+1]=temp;

​        }

​      }

​    }

​    

快速排序由于排序效率在同为O（N*logN）的的几种排序方法中效率较高，因此经常被采用，再加上快速排序思想----分治法也确实实用，

因此很多软件公司的笔试面试，包括像腾讯，微软等知名IT公司都喜欢考这个，还有大大小的程序方面的考试如软考，考研中也常常出现快速排序的身影。

该方法的基本思想是：

1.先从数列中取出一个数作为基准数。

2.分区过程，将比这个数大的数全放到它的右边，小于或等于它的数全放到它的左边。

3.再对左右区间重复第二步，直到各区间只有一个数。    

虽然快速排序称为分治法，但分治法这三个字显然无法很好的概括快速排序的全部步骤因此我的对快速排序作了进一步的说明：挖坑填数+分治法：

 

快速排序：

public class QuickSortTest {

​    public static void QuickSort(Integer ar[]) {

​        Integer a[] = ar.clone();

​        long currentTime = System.currentTimeMillis();

​        quick(a);

​        long nowTime = System.currentTimeMillis();

​        System.out.println("QuickSort-----------cost time:" + (nowTime - currentTime));

​        System.out.println(Arrays.toString( a));

​    }

​    public static int getMiddle(Integer[] list, int low, int high) {

​        int tmp = list[low]; // 数组的第一个作为中轴

​        while (low < high) {

​            while (low < high && list[high] >= tmp) {

​                high--;

​            }

​            list[low] = list[high]; // 比中轴小的记录移到低端

​            while (low < high && list[low] <= tmp) {

​                low++;

​            }

​            list[high] = list[low]; // 比中轴大的记录移到高端

​        }

​        list[low] = tmp; // 中轴记录到尾

​        return low; // 返回中轴的位置

​    }

​    public static void _quickSort(Integer[] list, int low, int high) {

​        if (low < high) {

​            int middle = getMiddle(list, low, high); // 将list数组进行一分为二

​            _quickSort(list, low, middle - 1); // 对低字表进行递归排序

​            _quickSort(list, middle + 1, high); // 对高字表进行递归排序

​        }

​    }

​    public static void quick(Integer[] a2) {

​        if (a2.length > 0) { // 查看数组是否为空

​            _quickSort(a2, 0, a2.length - 1);

​        }

​    }

​    public static void main(String[] args) {

​        Integer ar[] = new Integer[]{1,3,4,5,2,1,3,4,5};

​        QuickSort(ar);

​    }

}

https://blog.csdn.net/gaolei1201/article/details/51543618#commentBox

 

https://www.jianshu.com/p/5e171281a387

​    

 

 

=======================================================================mybatis中 参数注入 去引号=======================================================================

order by id #{order}   :  order by id 'asc'

order by id ${order}   :  order by id asc

 

 

使用#传入参数是，sql语句解析是会加上"",#{}传参能防止sql注入，如果你传入的参数为 单引号'，那么如果使用${},这种方式 那么是会报错的，

 

=======================================================================四舍五入  精度丢失  BigDecimal=======================================================================

BigDecimal bdTest = new BigDecimal(1.745);

BigDecimal bdTest1 = new BigDecimal(0.745);

bdTest = bdTest.setScale(2, BigDecimal.ROUND_HALF_UP);

bdTest1 = bdTest1.setScale(2, BigDecimal.ROUND_HALF_UP);

System.out.println("bdTest:" + bdTest); // 1.75

System.out.println("bdTest1:" + bdTest1); // 0.74

 

运行以上代码可以看到，1.745四舍五入的结果是1.75，0.745四舍五入的结果是0.74。

原因：

使用参数为float或double的BigDecimal创建对象会丢失精度。因此强烈建议不要使用参数为float或double的BigDecimal创建对象。

 

System.out.println(new BigDecimal(1.745)); // 1.74500000000000010658141036401502788066864013671875

System.out.println(new BigDecimal(0.745)); // 0.74499999999999999555910790149937383830547332763671875

 

 

解决办法：

\1. 使用BigDecimal(String val)的构造方法创建对象

new BigDecimal("1.745");

new BigDecimal("0.745");

\2. 使用使用BigDecimal的valueOf(double val)方法创建对象

BigDecimal.valueOf(1.745);

BigDecimal.valueOf(0.745);

 

 

有小数点的值，不论加减乘除，如果不添加双引号，会发生丢失精度的情况；

比如BigDecimal bd= new BigDecimal(0.48);

 

 

/**  

\* 提供精确的加法运算。  

*/  

public static double add(double v1,double v2){   

BigDecimal b1 = new BigDecimal(Double.toString(v1));   

BigDecimal b2 = new BigDecimal(Double.toString(v2));   

return b1.add(b2).doubleValue();   

}   

 

/**  

\* 提供精确的减法运算。  

*/  

public static double sub(double v1,double v2){   

BigDecimal b1 = new BigDecimal(Double.toString(v1));   

BigDecimal b2 = new BigDecimal(Double.toString(v2));   

return b1.subtract(b2).doubleValue();   

}   

 

/**  

\* 提供精确的乘法运算。  

*/  

public static double mul(double v1,double v2){   

BigDecimal b1 = new BigDecimal(Double.toString(v1));   

BigDecimal b2 = new BigDecimal(Double.toString(v2));   

return b1.multiply(b2).doubleValue();   

}

 

 

/**  

\* 提供（相对）精确的除法运算。当发生除不尽的情况时，由scale参数指  

\* 定精度，以后的数字四舍五入。  

\* @param v1 被除数  

\* @param v2 除数  

\* @param scale 表示表示需要精确到小数点以后几位。  

\* @return 两个参数的商  

*/  

public static double div(double v1,double v2,int scale){   

if(scale<0){   

throw new IllegalArgumentException(   

"The scale must be a positive integer or zero");   

}   

BigDecimal b1 = new BigDecimal(Double.toString(v1));   

BigDecimal b2 = new BigDecimal(Double.toString(v2));   

return b1.divide(b2,scale,BigDecimal.ROUND_HALF_UP).doubleValue();   

}      

 

 

/**  

\* 提供精确的小数位四舍五入处理。  

\* @param v 需要四舍五入的数字  

\* @param scale 小数点后保留几位  

\* @return 四舍五入后的结果  

*/  

public static double round(double v,int scale){   

if(scale<0){   

throw new IllegalArgumentException("The scale must be a positive integer or zero");   

}   

BigDecimal b = new BigDecimal(Double.toString(v));   

BigDecimal one = new BigDecimal("1");   

return b.divide(one,scale,BigDecimal.ROUND_HALF_UP).doubleValue();   

}   

};  

 

友情提示（丢失精度的原因）：

有小数点的值，不论加减乘除，如果不添加双引号，会发生丢失精度的情况；

比如BigDecimal bd= new BigDecimal(0.48);

 

 

=======================================================================在 Java 的反射中，Class.forName 和 ClassLoader 的区别=====================================================================

在java中Class.forName()和ClassLoader都可以对类进行加载。

Class.forName(String className)；在这个forName0方法中的第二个参数被默认设置为了true，这个参数代表是否对加载的类进行初始化，设置为true时会类进行初始化，代表会执行类中的静态代码块，以及对静态变量的赋值等操作。

也可以调用Class.forName(String name, boolean initialize,ClassLoader loader)方法来手动选择在加载类的时候是否要对类进行初始化。如果参数为true，则加载的类将会被初始化。

 

下面还是举例来说明结果吧：

一个含有静态代码块、静态变量、赋值给静态变量的静态方法的类

 

public class ClassForName {

​    //静态代码块

​    static {

​        System.out.println("执行了静态代码块");

​    }

​    //静态变量

​    private static String staticFiled = staticMethod();

​    //赋值静态变量的静态方法

​    public static String staticMethod(){

​        System.out.println("执行了静态方法");

​        return "给静态字段赋值了";

​    }

}

 

public class MyTest {

​    @Test

​    public void test44(){

​        try {

​            Class.forName("com.test.mytest.ClassForName");

​            System.out.println("#########分割符(上面是Class.forName的加载过程，下面是ClassLoader的加载过程)##########");

​            ClassLoader.getSystemClassLoader().loadClass("com.test.mytest.ClassForName");

​        } catch (ClassNotFoundException e) {

​            e.printStackTrace();

​        }

​    }

}

 

运行结果：

执行了静态代码块

执行了静态方法

\#########分割符(上面是Class.forName的加载过程，下面是ClassLoader的加载过程)##########

 

根据运行结果得出Class.forName加载类是将类进了初始化，而ClassLoader的loadClass并没有对类进行初始化，只是把类加载到了虚拟机中。

 

应用场景

在我们熟悉的Spring框架中的IOC的实现就是使用的ClassLoader。

而在我们使用JDBC时通常是使用Class.forName()方法来加载数据库连接驱动。这是因为在JDBC规范中明确要求Driver(数据库驱动)类必须向DriverManager注册自己。

 

 

 

=======================================================================  单例模式的七种写法=======================================================================

第一种（懒汉，线程不安全）：

public class Singleton {  

​    private static Singleton instance;  

​    private Singleton (){}  

 

​    public static Singleton getInstance() {  

​    if (instance == null) {  

​        instance = new Singleton();  

​    }  

​    return instance;  

​    }  

}  

 

第二种（懒汉，线程安全）：遗憾的是，效率很低，99%情况下不需要同步。

public class Singleton {  

​    private static Singleton instance;  

​    private Singleton (){}  

​    public static synchronized Singleton getInstance() {  

​    if (instance == null) {  

​        instance = new Singleton();  

​    }  

​    return instance;  

​    }  

}  

 

第三种（饿汉）：初始化instance显然没有达到lazy loading的效果。

public class Singleton {  

​    private static Singleton instance = new Singleton();  

​    private Singleton (){}  

​    public static Singleton getInstance() {  

​    return instance;  

​    }  

}  

 

第四种（饿汉，变种）：其实更第三种方式差不多，都是在类初始化即实例化instance。

public class Singleton {  

​    private Singleton instance = null;  

​    static {  

​    instance = new Singleton();  

​    }  

​    private Singleton (){}  

​    public static Singleton getInstance() {  

​    return this.instance;  

​    }  

}  

 

第六种（枚举）：

public enum Singleton {  

​    INSTANCE;  

​    public void whateverMethod() {  

​    }  

}  

这种方式是Effective Java作者Josh Bloch 提倡的方式，它不仅能避免多线程同步问题，而且还能防止反序列化重新创建新的对象，可谓是很坚强的壁垒啊

 

 

第七种（双重校验锁）：  JDK1.5已经没有双重检查锁定的问题了。

public class Singleton {  

​    private volatile static Singleton singleton;  

​    private Singleton (){}  

​    public static Singleton getSingleton() {  

​    if (singleton == null) {  

​        synchronized (Singleton.class) {  

​        if (singleton == null) {  

​            singleton = new Singleton();  

​        }  

​        }  

​    }  

​    return singleton;  

​    }  

}  

 

 

 

有两个问题需要注意：

1.如果单例由不同的类装载器装入，那便有可能存在多个单例类的实例。假定不是远端存取，例如一些servlet容器对每个servlet使用完全不同的类装载器，这样的话如果有两个servlet访问一个单例类，它们就都会有各自的实例。

2.如果Singleton实现了java.io.Serializable接口，那么这个类的实例就可能被序列化和复原。不管怎样，如果你序列化一个单例类的对象，接下来复原多个那个对象，那你就会有多个单例类的实例。单例与序列化的那些事儿

对第一个问题修复的办法是：

private static Class getClass(String classname)  

throws ClassNotFoundException {  

​    ClassLoader classLoader = Thread.currentThread().getContextClassLoader();

​    if(classLoader == null)     

​          classLoader = Singleton.class.getClassLoader();     

​          return (classLoader.loadClass(classname));     

​    }     

}  

对第二个问题修复的办法是：

public class Singleton implements java.io.Serializable {     

   public static Singleton INSTANCE = new Singleton();     

   protected Singleton() {     

   }     

   private Object readResolve() {     

​            return INSTANCE;     

   }    

}   

 

 

 

 

 

破坏单例性：http://www.importnew.com/29338.html

反射是可以破坏单例属性的。因为我们通过反射把它的构造函数设成可访问的，然后去生成一个新的对象。

通过对序列化后的Elvis 进行反序列化得到的对象是一个新的对象，这就破坏了Elvis 的单例性。序列化会通过反射调用无参数的构造方法创建一个新的对象。

 

http://www.importnew.com/29343.html

 

 

=======================================================================  JVM面试题 =======================================================================  

http://www.importnew.com/29299.html

http://www.importnew.com/29224.html

 

=======================================================================  SpringAOP =======================================================================  

http://www.importnew.com/29281.html

 

=======================================================================CompletableFuture=======================================================================

Future是Java5添加的类，用来描述一个异步计算的结果。

可以用isDone方法来检查计算是否完成，或者使用get阻塞住调用线程，直至计算完成返回结果，也可以用cancel方法来停止任务的执行。

Future以及相关使用方法提供了异步执行任务的能力，但对于结果的获取却是不方便，只能通过阻塞或轮询的方式得到任务结果。(Future.get会阻塞)

阻塞的方式与我们理解的异步编程其实是相违背的，而轮询又会耗无谓的CPU资源。而且还不能及时得到计算结果，为什么不能用观察者设计模式当计算结果完成及时通知监听者呢？

Java8里面新增加了一个包含50个方法左右的类：CompletableFuture. 提供了非常强大的Future的扩展功能

 

CompletableFuture 类实现了CompletionStage和Future接口，所以还是可以像以前一样通过阻塞或轮询的方式获得结果。尽管这种方式不推荐使用。

public T     get()

public T     get(long timeout, TimeUnit unit)

public T     getNow(T valueIfAbsent)

public T     join()

 

其中的getNow有点特殊，如果结果已经计算完则返回结果或抛异常，否则返回给定的valueIfAbsent的值。

 

Future可以代表在另外的线程中执行一段异步代码

Future可以代表在另外的线程中执行一段异步代码

Future可以代表在另外的线程中执行一段异步代码

尽管Future可以代表在另外的线程中执行一段异步代码，但你还是可以在本身线程中执行：

 

http://www.importnew.com/28319.html

https://www.cnblogs.com/cjsblog/p/9267163.html

https://blog.csdn.net/u011726984/article/details/79320004

https://blog.csdn.net/cainiao_user/article/details/76423495#commentBox

http://www.importnew.com/16149.html

 

CompletableFuture：它可能代表一个明确完成的Future，也有可能代表一个完成阶段（ CompletionStage ），它支持在计算完成以后触发一些函数或执行某些动作。

四个静态方法用来为一段异步执行的代码创建CompletableFuture对象：

public static CompletableFuture<Void>     runAsync(Runnable runnable)

public static CompletableFuture<Void>     runAsync(Runnable runnable, Executor executor)

public static <U> CompletableFuture<U>     supplyAsync(Supplier<U> supplier)

public static <U> CompletableFuture<U>     supplyAsync(Supplier<U> supplier, Executor executor)

 

 

CompletableFuture可以作为monad(单子)和functor. 由于回调风格的实现，我们不必因为等待一个计算完成而阻塞着调用线程，而是告诉CompletableFuture当计算完成的时候请执行某个Function. 还可以串联起来。

 

public <U> CompletableFuture<U>     thenApply(Function<? super T,? extends U> fn)

public <U> CompletableFuture<U>     thenApplyAsync(Function<? super T,? extends U> fn)

public <U> CompletableFuture<U>     thenApplyAsync(Function<? super T,? extends U> fn, Executor executor)

 

=======================================================================并行流=======================================================================

并行流 : 就是把一个内容分成多个数据块，并用不同的线程分 别处理每个数据块的流。

Stream API 可以声明性地通过 parallel() 与 sequential() 在并行流与顺序流之间进行切换。

 

 

=======================================================================Java7/8 中的 HashMap 和 ConcurrentHashMap 全解析=======================================================================

http://www.importnew.com/28263.html

 

 

=======================================================================BlockingQueue 实现之 SynchronousQueue=======================================================================

为什么说是同步的呢？这里说的并不是多线程的并发问题，而是因为当一个线程往队列中写入一个元素时，写入操作不会立即返回，需要等待另一个线程来将这个元素拿走；

同理，当一个读线程做读操作的时候，同样需要一个相匹配的写线程的写操作。这里的 Synchronous 指的就是读线程和写线程需要同步，一个读线程匹配一个写线程。

 

虽然上面我说了队列，但是 SynchronousQueue 的队列其实是虚的，其不提供任何空间（一个都没有）来存储元素。数据必须从某个写线程交给某个读线程，而不是写到某个队列中等待被消费。

你不能在 SynchronousQueue 中使用 peek 方法（在这里这个方法直接返回 null），peek 方法的语义是只读取不移除，显然，这个方法的语义是不符合 SynchronousQueue 的特征的。SynchronousQueue 也不能被迭代，因为根本就没有元素可以拿来迭代的。虽然 SynchronousQueue 间接地实现了 Collection 接口，但是如果你将其当做 Collection 来用的话，那么集合是空的。当然，这个类也是不允许传递 null 值的

 

 

=======================================================================java volatile关键字解惑=======================================================================

内存可见性：通俗来说就是，线程A对一个volatile变量的修改，对于其它线程来说是可见的，即线程每次获取volatile变量的值都是最新的。

 

使用volatile必须满足两个条件：

1、对变量的写操作不依赖当前值，如多线程下执行a++，是无法通过volatile保证结果准确性的；

2、该变量没有包含在具有其它变量的不变式中，这句话有点拗口，看代码比较直观。

public class NumberRange {

​    private volatile int lower = 0;

​     private volatile int upper = 10;

 

​    public int getLower() { return lower; }

​    public int getUpper() { return upper; }

 

​    public void setLower(int value) {

​        if (value > upper)

​            throw new IllegalArgumentException(...);

​        lower = value;

​    }

 

​    public void setUpper(int value) {

​        if (value < lower)

​            throw new IllegalArgumentException(...);

​        upper = value;

​    }

}

上述代码中，上下界初始化分别为0和10，假设线程A和B在某一时刻同时执行了setLower(8)和setUpper(5)，且都通过了不变式的检查，设置了一个无效范围（8, 5），所以在这种场景下，需要通过sychronize保证方法setLower和setUpper在每一时刻只有一个线程能够执行。

 

 

下面是我们在项目中经常会用到volatile关键字的两个场景：

1、状态标记量

public class ServerHandler {

​    private volatile isopen;

​    public void run() {

​        if (isopen) {

​           //促销逻辑

​        } else {

​          //正常逻辑

​        }

​    }

​    public void setIsopen(boolean isopen) {

​        this.isopen = isopen

​    }

}

用户的请求线程执行run方法，如果需要开启促销活动，可以通过后台设置，具体实现可以发送一个请求，调用setIsopen方法并设置isopen为true，由于isopen是volatile修饰的，所以一经修改，其他线程都可以拿到isopen的最新值，用户请求就可以执行促销逻辑了。

 

2、double check

单例模式的一种实现方式，但很多人会忽略volatile关键字，因为没有该关键字，程序也可以很好的运行，只不过代码的稳定性总不是100%，说不定在未来的某个时刻，隐藏的bug就出来了。

class Singleton {

​    private volatile static Singleton instance;

​    public static Singleton getInstance() {

​        if (instance == null) {

​            syschronized(Singleton.class) {

​                if (instance == null) {

​                    instance = new Singleton();

​                }

​            }

​        }

​        return instance;

​    }

}

不过在众多单例模式的实现中，我比较推荐懒加载的优雅写法Initialization on Demand Holder（IODH）。

 

public class Singleton {  

​    static class SingletonHolder {  

​        static Singleton instance = new Singleton();  

​    }  

​      

​    public static Singleton getInstance(){  

​        return SingletonHolder.instance;  

​    }  

}  

当然，如果不需要懒加载的话，直接初始化的效果更好。

 

如何保证内存可见性？

在java虚拟机的内存模型中，有主内存和工作内存的概念，每个线程对应一个工作内存，并共享主内存的数据，下面看看操作普通变量和volatile变量有什么不同：

 

1、对于普通变量：读操作会优先读取工作内存的数据，如果工作内存中不存在，则从主内存中拷贝一份数据到工作内存中；写操作只会修改工作内存的副本数据，这种情况下，其它线程就无法读取变量的最新值。

2、对于volatile变量，读操作时JMM会把工作内存中对应的值设为无效，要求线程从主内存中读取数据；写操作时JMM会把工作内存中对应的数据刷新到主内存中，这种情况下，其它线程就可以读取变量的最新值。

这段文字显得有点苍白无力，不如来段简明的代码：

 

class Singleton {

​    private volatile static Singleton instance;

​    private int a;

​    private int b;

​    private int b;

​    public static Singleton getInstance() {

​        if (instance == null) {

​            syschronized(Singleton.class) {

​                if (instance == null) {

​                    a = 1;  // 1

​                     b = 2;  // 2

​                    instance = new Singleton();  // 3

​                    c = a + b;  // 4

​                }

​            }

​        }

​        return instance;

​    }

}

 

1、如果变量instance没有volatile修饰，语句1、2、3可以随意的进行重排序执行，即指令执行过程可能是3214或1324。

2、如果是volatile修饰的变量instance，会在语句3的前后各插入一个内存屏障。

 

通过观察volatile变量和普通变量所生成的汇编代码可以发现，操作volatile变量会多出一个lock前缀指令：

 

Java代码：

instance = new Singleton();

 

汇编代码：

0x01a3de1d: movb $0x0,0x1104800(%esi);

0x01a3de24: **lock** addl $0x0,(%esp);

 

这个lock前缀指令相当于上述的内存屏障，提供了以下保证：

1、将当前CPU缓存行的数据写回到主内存；

2、这个写回内存的操作会导致在其它CPU里缓存了该内存地址的数据无效。

 

CPU为了提高处理性能，并不直接和内存进行通信，而是将内存的数据读取到内部缓存（L1，L2）再进行操作，但操作完并不能确定何时写回到内存，如果对volatile变量进行写操作，当CPU执行到Lock前缀指令时，会将这个变量所在缓存行的数据写回到内存，不过还是存在一个问题，就算内存的数据是最新的，其它CPU缓存的还是旧值，所以为了保证各个CPU的缓存一致性，每个CPU通过嗅探在总线上传播的数据来检查自己缓存的数据有效性，当发现自己缓存行对应的内存地址的数据被修改，就会将该缓存行设置成无效状态，当CPU读取该变量时，发现所在的缓存行被设置为无效，就会重新从内存中读取数据到缓存中。

 

 

=======================================================================面试必问的 CAS=======================================================================

CAS（Compare and Swap），即比较并替换，实现并发算法时常用到的一种技术，Doug lea大神在java同步器中大量使用了CAS技术，鬼斧神工的实现了多线程执行的安全性。

CAS的思想很简单：三个参数，一个当前内存值V、旧的预期值A(手里的当前值)、即将更新的值B，当且仅当预期值A和内存值V相同时，将内存值修改为B并返回true，否则什么都不做，并返回false。

 

JDK自带的CAS方案，在CAS中，比较和替换是一组原子操作，不会被外部打断，且在性能上更占有优势。

 

下面以AtomicInteger的实现为例，分析一下CAS是如何实现的。

public class AtomicInteger extends Number implements java.io.Serializable {

​    // setup to use [Unsafe.compareAndSwapInt](http://unsafe.compareandswapint/) for updates

​    private static final Unsafe unsafe = Unsafe.getUnsafe();

​    private static final long valueOffset;

​    static {

​        try {

​            valueOffset = unsafe.objectFieldOffset

​                (AtomicInteger.class.getDeclaredField("value"));

​        } catch (Exception ex) { throw new Error(ex); }

​    }

​    private volatile int value;

​    public final int get() {return value;}

}

Unsafe，是CAS的核心类，由于Java方法无法直接访问底层系统，需要通过本地（native）方法来访问，Unsafe相当于一个后门，基于该类可以直接操作特定内存的数据。

变量valueOffset，表示该变量值在内存中的偏移地址，因为Unsafe就是根据内存偏移地址获取数据的。

变量value用volatile修饰，保证了多线程之间的内存可见性。

 

看看AtomicInteger如何实现并发下的累加操作：

public final int getAndAdd(int delta) {    

​    return unsafe.getAndAddInt(this, valueOffset, delta);

}

//unsafe.getAndAddInt

public final int getAndAddInt(Object var1, long var2, int var4) {

​    int var5;

​    do {

​        var5 = this.getIntVolatile(var1, var2);

​    } while(!this.compareAndSwapInt(var1, var2, var5, var5 + var4));

​    return var5;

}

 

AtomicInteger里面的value原始值为3，即主内存中AtomicInteger的value为3，根据Java内存模型，线程A和线程B各自持有一份value的副本，值为3。

线程A通过getIntVolatile(var1, var2)拿到value值3，这时线程A被挂起。

线程B也通过getIntVolatile(var1, var2)方法获取到value值3，运气好，线程B没有被挂起，并执行compareAndSwapInt方法比较内存值也为3，成功修改内存值为2。

这时线程A恢复，执行compareAndSwapInt方法比较，发现自己手里的值(3)和内存的值(2)不一致，说明该值已经被其它线程提前修改过了，那只能重新来一遍了。

重新获取value值，因为变量value被volatile修饰，所以其它线程对它的修改，线程A总是能够看到，线程A继续执行compareAndSwapInt进行比较替换，直到成功。

 

 

http://www.importnew.com/27596.html

 

 

public final boolean compareAndSet(int expect, int update) {

​     return unsafe.compareAndSwapInt(this, valueOffset, expect, update);

}

 

=======================================================================分布式锁=======================================================================

在分布式场景下，需要保证多个应用实例都能够执行同步代码，则需要做一些额外的工作，一个最典型分布式同步方案便是使用分布式锁。

 

分布式锁由很多种实现，但本质上都是类似的，即依赖于共享组件实现锁的询问和获取，如果说单体式应用中的Monitor是由JVM提供的，那么分布式下Monitor便是由共享组件提供，而典型的共享组件大家其实并不陌生，包括但不限于：Mysql，Redis，Zookeeper。同时他们也代表了三种类型的共享组件：数据库，缓存，分布式协调组件。基于Consul的分布式锁，其实和基于Zookeeper的分布式锁大同小异，都是借助于分布式协调组件实现锁，大而化之，这三种类型的分布式锁，原理也都差不多，只不过，锁的特性和实现细节有所差异。

 

http://www.importnew.com/27278.html

 

构造器中的计数值（count）实际上就是闭锁需要等待的线程数量。这个值只能被设置一次，而且CountDownLatch没有提供任何机制去重新设置这个计数值。

 

与CountDownLatch的第一次交互是主线程等待其他线程。主线程必须在启动其他线程后立即调用CountDownLatch.await()方法。这样主线程的操作就会在这个方法上阻塞，直到其他线程完成各自的任务。

 

其他N 个线程必须引用闭锁对象，因为他们需要通知CountDownLatch对象，他们已经完成了各自的任务。这种通知机制是通过 CountDownLatch.countDown()方法来完成的；每调用一次这个方法，在构造函数中初始化的count值就减1。所以当N个线程都调 用了这个方法，count的值等于0，然后主线程就能通过await()方法，恢复执行自己的任务。

 

=======================================================================Semaphore=======================================================================

CyclicBarrier和CountDownLatch的区别

CountDownLatch的计数器只能使用一次，而CyclicBarrier的计数器可以使用reset()方法重置。

 

Semaphore

Semaphore(信号量)是用来控制同事访问特定资源的线程数量，它协调各个线程，以保证合理的使用公共资源。Semaphore有两个构造函数：Semaphore(int permits)默认是非公平的，Semaphore(int permits, boolean fair)可以设置为公平的。应用案例如下：

 

Semaphore(信号量)是用来控制同事访问特定资源的线程数量，它协调各个线程，以保证合理的使用公共资源。Semaphore有两个构造函数：Semaphore(int permits)默认是非公平的，Semaphore(int permits, boolean fair)可以设置为公平的。应用案例如下：

public class SemaphoreTest

{

​    private static final int THREAD_COUNT=30;

​    private static ExecutorService threadPool = Executors.newFixedThreadPool(30);

​    private static Semaphore s = new Semaphore(10);

​    public static void main(String[] args)

​    {

​        for(int i=0;i<THREAD_COUNT;i++)

​        {

​            final int a = i;

​            threadPool.execute(new Runnable(){

​                @Override

​                public void run()

​                {

​                    try

​                    {

​                        s.acquire();

​                        System.out.println("do something...."+a);

​                        s.release();

​                    }

​                    catch (InterruptedException e)

​                    {

​                        e.printStackTrace();

​                    }

​                }

​            });

​        }

​        threadPool.shutdown();

​    }

}

 

由上例可以看出Semaphore的用法非常的简单，首先线程使用Semaphore的acquire()方法获取一个许可证，使用完之后调用release()方法归还许可证。还可以用tryAcquire()方法尝试获取许可证。Semaphore还提供了一些其他方法： int availablePermits()返回此信号量中当前可用的许可证数；int getQueueLength()返回正在等待获取许可证的线程数；boolean hasQueuedThreads()是否有线程正在等待获取许可证；void reducePermits(int reduction)减少reduction个许可证，是个protected方法；Collection<Thread> getQueuedThreads()返回所有等待获取许可证的线程集合，也是一个protected方法。

 

 

 

 

=======================================================================线程间交换数据的Exchanger=======================================================================

Exchanger是一个用于线程间协作的工具类。Exchanger用于进行线程间的数据交换。它提供一个同步点，在这个同步点，两个线程可以交换彼此的数据。这两个线程通过exchange方法交换数据，如果第一个线程先执行exchange()方法，它会一直等待第二个线程也执行exchange方法。当两个线程都到达同步点时，这两个线程就可以交换数据，将本现场生产出来的数据传递给对方。

 

import java.util.concurrent.Exchanger;

import java.util.concurrent.ExecutorService;

import java.util.concurrent.Executors;

public class ExchangerTest

{

​    private static final Exchanger<String> exchanger = new Exchanger<>();

​    private static ExecutorService threadPool = Executors.newFixedThreadPool(2);

​    public static void main(String[] args)

​    {

​        threadPool.execute(new Runnable(){

​            @Override

​            public void run()

​            {

​                String A = "I'm A!";

​                try

​                {

​                    String B = exchanger.exchange(A);

​                    System.out.println("In 1-"+Thread.currentThread().getName()+": "+B);

​                }

​                catch (InterruptedException e)

​                {

​                    e.printStackTrace();

​                }

​            }

​        });

​        threadPool.execute(new Runnable(){

​            @Override

​            public void run()

​            {

​                try

​                {

​                    String B="I'm B!";

​                    String A = exchanger.exchange(B);

​                    System.out.println("In 2-"+Thread.currentThread().getName()+": "+A);

​                }

​                catch (InterruptedException e)

​                {

​                    e.printStackTrace();

​                }

​            }

​        });

​        threadPool.shutdown();

​    }

}

 

 

输出结果：

In 2-pool-1-thread-2: I'm A!

In 1-pool-1-thread-1: I'm B!

 

如果两个线程有一个没有执行exchange(V x)方法，则会一直等待，如果担心有特殊情况发生，避免一直等待，可以使用exchange(V x, long timeout, TimeUnit unit)设置最大等待时长。

 

 

=======================================================================扩展ThreadPoolExecutor=======================================================================

可以通过继承线程池来自定义线程池，重写线程池的beforeExecute, afterExecute和terminated方法。在执行任务的线程中将调用beforeExecute和afterExecute等方法，在这些方法中还可以添加日志、计时、监视或者统计信息收集的功能。无论任务是从run中正常返回，还是抛出一个异常而返回，afterExecute都会被调用。如果任务在完成后带有一个Error，那么就不会调用afterExecute。如果beforeExecute抛出一个RuntimeException，那么任务将不被执行，并且afterExecute也不会被调用。在线程池完成关闭时调用terminated，也就是在所有任务都已经完成并且所有工作者线程也已经关闭后，terminated可以用来释放Executor在其生命周期里分配的各种资源，此外还可以执行发送通知、记录日志或者手机finalize统计等操作。

 

 

ThreadPoolExecutor是可扩展的，通过查看源码可以发现，它提供了几个可以在子类化中改写的方法：beforeExecute,afterExecute,terminated.

源码片段如下所示：

protected void beforeExecute(Thread t, Runnable r) { }

protected void afterExecute(Runnable r, Throwable t) { }

protected void terminated() { }

 

可以注意到，这三个方法都是protected的空方法，摆明了是让子类扩展的嘛。

在执行任务的线程中将调用beforeExecute和afterExecute等方法，在这些方法中还可以添加日志、计时、监视或者统计信息收集的功能。无论任务是从run中正常返回，还是抛出一个异常而返回，afterExecute都会被调用。如果任务在完成后带有一个Error，那么就不会调用afterExecute。如果beforeExecute抛出一个RuntimeException，那么任务将不被执行，并且afterExecute也不会被调用。

在线程池完成关闭时调用terminated，也就是在所有任务都已经完成并且所有工作者线程也已经关闭后，terminated可以用来释放Executor在其生命周期里分配的各种资源，此外还可以执行发送通知、记录日志或者手机finalize统计等操作。

 

public class TimingThreadPool extends ThreadPoolExecutor

{

​    private final ThreadLocal<Long> startTime = new ThreadLocal<Long>();

​    private final Logger log = Logger.getAnonymousLogger();

​    private final AtomicLong numTasks = new AtomicLong();

​    private final AtomicLong totalTime = new AtomicLong();

​    

​    public TimingThreadPool(int corePoolSize, int maximumPoolSize, long keepAliveTime, TimeUnit unit,

​            BlockingQueue<Runnable> workQueue)

​    {

​        super(corePoolSize, maximumPoolSize, keepAliveTime, unit, workQueue);

​    }

​    protected void beforeExecute(Thread t, Runnable r){

​        super.beforeExecute(t, r);

​        log.info(String.format("Thread %s: start %s", t,r));

​        startTime.set(System.nanoTime());

​    }

​    

​    protected void afterExecute(Runnable r, Throwable t){

​        try{

​            long endTime = System.nanoTime();

​            long taskTime = endTime-startTime.get();

​            numTasks.incrementAndGet();

​            totalTime.addAndGet(taskTime);

​            log.info(String.format("Thread %s: end %s, time=%dns", t,r,taskTime));

​        }

​        finally

​        {

​            super.afterExecute(r, t);

​        }

​    }

​    

​    protected void terminated()

​    {

​        try

​        {

​            log.info(String.format("Terminated: avg time=%dns",totalTime.get()/numTasks.get()));

​        }

​        finally

​        {

​            super.terminated();

​        }

​    }

}

 

 

=======================================================================CompletionService=======================================================================

如果想Executor提交了一组计算任务，并且希望在计算完成后获得结果，那么可以保留与每个任务关联的Future，然后反复使用get方法，同事将参数timeout指定为0，从而通过轮询来判断任务是否完成。这种方法虽然可行，但却有些繁琐。幸运的是，还有一种更好的方法：CompletionService。CompletionService将Executor和BlockingQueue的功能融合在一起。你可以将Callable任务提交给它来执行，然后使用类似于队列操作的take和poll等方法来获得已完成的结果，而这些结果会在完成时被封装为Future。ExecutorCompletionService实现了CompletionService,并将计算部分委托到一个Executor。代码示例如下：

 

int coreNum = Runtime.getRuntime().availableProcessors();

ExecutorService executor = Executors.newFixedThreadPool(coreNum);

CompletionService<Object> completionService = new ExecutorCompletionService<Object>(executor);

for(int i=0;i<coreNum;i++)

{

​    completionService.submit( new Callable<Object>(){

​        @Override

​        public Object call() throws Exception

​        {

​            return Thread.currentThread().getName();

​        }});

}

for(int i=0;i<coreNum;i++)

{

​    try

​    {

​        Future<Object> future = completionService.take();

​        System.out.println(future.get());

​    }

​    catch (InterruptedException | ExecutionException e)

​    {

​        e.printStackTrace();

​    }

}

 

运行结果：

pool-1-thread-1

pool-1-thread-2

pool-1-thread-3

pool-1-thread-4

 

 

 

=======================================================================CAS ABA问题=======================================================================

ABA问题

ABA问题发生在类似这样的场景：线程1转变使用CAS将变量A的值替换为C，在此时，线程2将变量的值由A替换为C，又由C替换为A，然后线程1执行CAS时发现变量的值仍为A，所以CAS成功。但实际上这时的现场已经和最初的不同了。大多数情况下ABA问题不会产生什么影响。如果有特殊情况下由于ABA问题导致，可用采用AtomicStampedReference来解决，原理：乐观锁+version。可以参考下面的案例来了解其中的不同。

public class ABAQuestion

{

​    private static AtomicInteger atomicInt = new AtomicInteger(100);

​    private static AtomicStampedReference<Integer> atomicStampedRef = new AtomicStampedReference<Integer>(100,0);

​    public static void main(String[] args) throws InterruptedException

​    {

​        Thread thread1 = new Thread(new Runnable(){

​            @Override

​            public void run()

​            {

​                atomicInt.compareAndSet(100, 101);

​                atomicInt.compareAndSet(101, 100);

​            }

​        });

​        Thread thread2 = new Thread(new Runnable(){

​            @Override

​            public void run()

​            {

​                try

​                {

​                    TimeUnit.SECONDS.sleep(1);

​                }

​                catch (InterruptedException e)

​                {

​                    e.printStackTrace();

​                }

​                boolean c3 = atomicInt.compareAndSet(100, 101);

​                System.out.println(c3);

​            }

​        });

​        thread1.start();

​        thread2.start();

​        thread1.join();

​        thread2.join();

​        Thread thread3 = new Thread(new Runnable(){

​            @Override

​            public void run()

​            {

​                try

​                {

​                    TimeUnit.SECONDS.sleep(1);

​                }

​                catch (InterruptedException e)

​                {

​                    e.printStackTrace();

​                }

​                atomicStampedRef.compareAndSet(100, 101, atomicStampedRef.getStamp(), atomicStampedRef.getStamp()+1);

​                atomicStampedRef.compareAndSet(101, 100, atomicStampedRef.getStamp(), atomicStampedRef.getStamp()+1);

​            }

​        });

​        Thread thread4 = new Thread(new Runnable(){

​            @Override

​            public void run()

​            {

​                int stamp = atomicStampedRef.getStamp();

​                try

​                {

​                    TimeUnit.SECONDS.sleep(2);

​                }

​                catch (InterruptedException e)

​                {

​                    e.printStackTrace();

​                }

​                boolean c3 = atomicStampedRef.compareAndSet(100, 101, stamp, stamp+1);

​                System.out.println(c3);

​            }

​        });

​        thread3.start();

​        thread4.start();

​    }

}

 

 

=======================================================================Spring Batch=======================================================================

简单的批处理,复杂的大数据批处理作业都可以通过SpringBatch框架来实现。

 

spring batch官方文档：https://docs.spring.io/spring-batch

spring batch3.x中文文档：http://www.kailing.pub/SpringBatchReference

spring batch官方入门实例：https://projects.spring.io/spring-batch/

 

所有的批处理都可以描述为最简单的过程：读取大量数据，执行自定义的计算或者转换，写出处理结果，SpringBatch提供了三个主要接口来执行大量数据的读取、处理与写出：ItemReader、ItemProcessor、ItemWriter。

 

ItemReader

ItemReader就是一种从各个数据源读取数据，然后提供给后续步骤 使用的接口，目前SpringBatch已经给我们实现了3种常用格式的处理：

1）Flat平面纯文本处理，FlatFileItemReader类实现了从纯文本文件中读取一行数据，目前支持三种格式处理：定长字符串处理、分隔符字符串处理、正则表达式字符串处理，这三种处理基本能够满足我们常见需求了，而且常见的批量数据也都是格式化的纯文本；

2）XML，XMLItemReader类提供了解析、验证、映射数据的功能，能够对XML进行处理，同时可以根据XSD schema验证格式信息是否正确；

3）数据库，SQLItemReader类实现了通过JDBC查询出数据集，然后进行数据处理；

如果上面提供的三种都不能满足要求，还可以自己去实现IteamReader接口，来完成从字符串到实体对象的转换：

package org.springframework.batch.item;

public interface ItemReader<T> {

​    T read() throws Exception, UnexpectedInputException, ParseException, NonTransientResourceException;

}

 

ItemWriter

ItemWriter功能上类似ItemReader的反向操作，资源任需要定位、打开和关闭，区别ItemWriter执行的是写入操作，而不是读取；

框架同样也实现了类似Reader的常用Writer类，FlatFileItemWriter、XMLItemWriter、SQLItemWriter

如果这几个常用Writer类满足不了你的需求那么你也可以继承ItemWriter自己去实现Writer类：

package org.springframework.batch.item;

import java.util.List;

public interface ItemWriter<T> {

​    void write(List<? extends T> var1) throws Exception;

}

 

ItemProcessor

ItemProcessor顾名思义就是数据的处理类，这个类系统没有实现类，因为是否需要对数据进行处理，对数据如何处理都是开发者自己来决定的，所以这里框架只是提供了接口，让大家去实现ItemProcessor接口中的process方法。

package org.springframework.batch.item;

public interface ItemProcessor<I, O> {

​    O process(I var1) throws Exception;

}

从接口我们可以看到ItemProcessor是一个双范型接口，需要设置输入和输出类型，第一个类型为我们ItemReader的输出类型，第二个类型为ItemWriter的输入类型也就是process方法按照开发者的意愿处理后输出的类型。

 

 

下面我们直接来实战，实现一个功能，大家就会很快上手SpringBatch了，这里我们实现到指定目录读取支付宝和微信的账单并处理后输出到指定的文件，这里我们没有使用数据库，如果要使用数据库只需要设置writer里的datasource并使用SQL相关的writer类就可以了

 

定义的阿里账单实体类，省略了setter、getter方法。

public class AlipayTranDO {

​    private String tranId;

​    private String channel;

​    private String tranType;

​    private String counterparty;

​    private String goods;

​    private String amount;

​    private String isDebitCredit;

​    private String state;

...

}

 

 

 

实体类HopPayTranDO

public class HopPayTranDO {

​    private String tranId;

​    private String channel;

​    private String tranType;

​    private String counterparty;

​    private String goods;

​    private String amount;

​    private String isDebitCredit;

​    private String state;

​    private String tranDate;

​    private String merId;

  ...

}

 

支付宝账单Reader类:

Reader类中核心实现是通过FlatFileItemReader来处理支付宝账单单条文本记录，csv的文本记录包含了8个字段，分别通过逗号分隔，然后与AlipayTranDO类属性字段映射，必须保证同名；通过setLineTokenizer（）设置行分割方式和分割字段；通过setFieldSetMapper（）方法设置读取字段映射的类为AlipayTranDO.class，整体过程还是比较简单的；

 

在Reader类中还有一个getMultiAliReader()方法，该方法是获取多个文件作为Resource，让上面定义的FlatFileItemReader<AlipayTranDO>去对每个文件的每条记录单独处理，网上绝大多数的例子都是只处理一个文件，实际使用过程中不可能只处理一个批量文件，所以例子中我引入了MultiResourceItemReader类，该类是SpringBatch中用于处理多文件的情况，通过给MultiResourceItemReader设置Resource数组，并通过setDelegate设置处理单文件单Item的类实例，最后将该多文件读取的ItemReader配置在Job中即可实现多文件的读取功能。

 

public class AlipayFileItemReader {

 

​    private FlatFileItemReader<AlipayTranDO> reader;

 

​    public FlatFileItemReader<AlipayTranDO> getAlipayFileItemReader() {

​        reader = new FlatFileItemReader<AlipayTranDO>();

​        reader.setLineMapper(new DefaultLineMapper<AlipayTranDO>() {{

​            setLineTokenizer(new DelimitedLineTokenizer() {{

​                setNames(new String[] { "tranId", "channel", "tranType", "counterparty", "goods", "amount", "isDebitCredit", "state" });

​            }});

​            setFieldSetMapper(new BeanWrapperFieldSetMapper<AlipayTranDO>() {{

​                setTargetType(AlipayTranDO.class);

​            }});

​        }});

​        reader.setLinesToSkip(5);

​        return reader;

​    }

 

​    public MultiResourceItemReader<AlipayTranDO> getMultiAliReader() {

​        //TODO: 获取所有当天待加载的支付宝账单,

​        // 这里只是简单的放了两个csv账单文件，

​        // 实际处理过程中，肯定是从数据库或者接口获取需要加载的账单文件路径

​        MultiResourceItemReader<AlipayTranDO> reader = new MultiResourceItemReader<AlipayTranDO>();

​        Resource[] files = new Resource[]{new FileSystemResource("data/alipay/208012345_20141030.csv"),

​                new FileSystemResource("data/alipay/208054321_20141030.csv")};

​        reader.setResources(files);

​        reader.setDelegate(this.getAlipayFileItemReader());

 

​        return reader;

​    }

}

 

 

AlipayItemProcessor支付宝账单处理转换类

因为是例子，所以processor的处理过程比较简单，只是将从支付宝账单csv中读取的字段赋值给自己定义的内部聚合账单实体类，并多加工了两个字段，在实际的使用过程中大家可以按照自己系统批量加工的需求去处理加工字段；

 

public class AlipayItemProcessor implements ItemProcessor<AlipayTranDO, HopPayTranDO> {

 

​    private static final Logger log = LoggerFactory.getLogger(AlipayItemProcessor.class);

 

​    @Override

​    public HopPayTranDO process(AlipayTranDO alipayTranDO) throws Exception {

​        HopPayTranDO hopPayTranDO = new HopPayTranDO();

​        hopPayTranDO.setTranId(alipayTranDO.getTranId());

​        hopPayTranDO.setChannel(alipayTranDO.getChannel());

​        hopPayTranDO.setTranType(alipayTranDO.getTranType());

​        hopPayTranDO.setCounterparty(alipayTranDO.getCounterparty());

​        hopPayTranDO.setGoods(alipayTranDO.getGoods());

​        hopPayTranDO.setAmount(alipayTranDO.getAmount());

​        hopPayTranDO.setIsDebitCredit(alipayTranDO.getIsDebitCredit());

​        hopPayTranDO.setState(alipayTranDO.getState());

 

​        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");

​        String dateNowStr = sdf.format(new Date());

​        hopPayTranDO.setTranDate(dateNowStr);

​        hopPayTranDO.setMerId("00000001");

​        log.info(alipayTranDO.toString());

​        return hopPayTranDO;

​    }

}

 

 

AlipayFileItemWriter账单写入类

该文件写入类就是将刚才Processor输出的加工后的HopPayTranDO对象列表写入到文件中

public class AlipayFileItemWriter {

 

​    public FlatFileItemWriter<HopPayTranDO> getAlipayItemWriter() {

​        FlatFileItemWriter<HopPayTranDO> txtItemWriter = new FlatFileItemWriter<HopPayTranDO>();

​        txtItemWriter.setAppendAllowed(true);

​        txtItemWriter.setShouldDeleteIfExists(true);

​        txtItemWriter.setEncoding("UTF-8");

​        txtItemWriter.setResource(new FileSystemResource("data/sample-data.txt"));

​        txtItemWriter.setLineAggregator(new DelimitedLineAggregator<HopPayTranDO>() {{

​            setDelimiter(",");

​            setFieldExtractor(new BeanWrapperFieldExtractor<HopPayTranDO>() {{

​                setNames(new String[]{"tranId", "channel", "tranType", "counterparty", "goods", "amount", "isDebitCredit", "state", "tranDate", "merId" });

​            }});

​        }});

​        return txtItemWriter;

​    }

}

 

 

BillBatchConfig JOB配置类

 

Job配置比较简单，先将下面要用到的JobBuilderFactory、StepBuilderFactory、AlipayFileItemReader、AlipayItemProcessor、AlipayFileItemWriter先分别注入实例，再配置step步骤，如果有多个步骤可以在flow(step1)后面.next(step2)，对于简单的批量这样的线性设置步骤就可以满足要求了，如果涉及到复杂情况，我会再写一篇来介绍SpringBatch的高级应用来讲解，本篇就不赘述了。

 

@Configuration

@EnableBatchProcessing

public class BillBatchConfig {

 

​    @Autowired

​    public JobBuilderFactory jobBuilderFactory;

 

​    @Autowired

​    public StepBuilderFactory stepBuilderFactory;

 

​    @Autowired

​    private AlipayFileItemReader alipayFileItemReader;

 

​    @Autowired

​    private AlipayItemProcessor alipayItemProcessor;

 

​    @Autowired

​    private AlipayFileItemWriter alipayFileItemWriter;

 

​    @Bean

​    public Job importAliJob() {

​        return jobBuilderFactory.get("importAliJob")

​                .incrementer(new RunIdIncrementer())

​                .flow(step1())

​                .end()

​                .build();

​    }

 

​    @Bean

​    public Step step1() {

​        return stepBuilderFactory.get("step1")

​                .<AlipayTranDO, HopPayTranDO> chunk(10)

​                .reader(alipayFileItemReader.getMultiAliReader())

​                .processor(alipayItemProcessor)

​                .writer(alipayFileItemWriter.getAlipayItemWriter())

​                .build();

​    }

 

}

 

 

续基于Springbatch全程使用javaconfig的方式实现，数据加载入库、异常数据处理、并行、定时任务等:

 

https://www.jianshu.com/p/260159a0681b

 

 

 

=======================================================================CPU 100%=======================================================================

 

http://www.importnew.com/26413.html

 

 

 

 

 

 

 

=======================================================================再谈 CAS  ConcurrentHashMap=======================================================================

不加锁而实现操作原子化的一种巧妙的编程方式

CAS到底如何能够实现锁的功能呢？？？？？

 

拿a＋＋操作举例：

public final int getAndIncrement() {    

​    while (true) {    

​        int current = get();            

​        int next = current + 1;    

​        if (compareAndSet(current, next))    

​            return current;    

​    }    

}  

 

这里面的compareAndSet的功能为，a与current比较，如果相等则把a的值变为next；这时候可以保证在int next = current + 1;与if（）；之间不会被其他线程抢占（因为a的值在这段时间内没有变）

因为a的值在这段时间内没有变，因为a的值在这段时间内没有变，因为a的值在这段时间内没有变因为a的值在这段时间内没有变因为a的值在这段时间内没有变，因为a的值在这段时间内没有变

，如果被抢占则会做自旋操作。这就在某种程度上可以实现原子性操作。

 

即：  先获取操作之前的a的值，存到一个中间变量里，操作这个中间变量得到B。

​      如果中间变量 == a,则将a变成B。

​      

这是一种不加锁而实现操作原子化的一种巧妙的编程方式，不仅在Java的jvm种，甚至在操作系统的底层并发实现机制中也有CAS的大量应用。    

 

为什么a++会有线程安全问题，举例子：a初始值为1

 

有2个线程同时执行了 int current = get();    得到值： 0

有2个线程同时执行了 int next = current + 1; 得到值： 1

a = next；   线程1：a=0，current=0，则a=1。线程2： a=1，current=0，则会做自旋操作

 

 

 

例子走一波：

public class TestConcurrent {

​    private final static Map<String, Long> urlCounter = new ConcurrentHashMap<String, Long>();

 

​    // 接口调用次数+1

​    public long increase(String url) {

​        Long oldValue = urlCounter.get(url);

​        Long newValue = oldValue + 1;

​        urlCounter.put(url, newValue);

​        return newValue;

​    }

 

​    // 获取调用次数

​    public Long getCount(String url) {

​        return urlCounter.get(url);

​    }

 

​    public static void main(String[] args) {

​        ExecutorService executor = Executors.newFixedThreadPool(10);

​        final TestConcurrent counterDemo = new TestConcurrent();

​        int callTime = 1000;

​        final String url = "[http://localhost:8080/hello";](http://localhost:8080/hello)

​        urlCounter.put(url, 1L);

​        final CountDownLatch countDownLatch = new CountDownLatch(callTime);

​        // 模拟并发情况下的接口调用统计

​        for (int i = 0; i < callTime; i++) {

​            executor.execute(new Runnable() {

​                @Override

​                public void run() {

​                    counterDemo.increase(url);

​                    countDownLatch.countDown();

​                }

​            });

​        }

​        try {

​            countDownLatch.await();

​        } catch (InterruptedException e) {

​            e.printStackTrace();

​        }

​        executor.shutdown();

​        // 等待所有线程统计完成后输出调用次数

​        System.out.println("调用次数：" + counterDemo.getCount(url));

​    }

}

 

结果：810

 

Long oldValue = urlCounter.get(url);   2个线程同时得到oldValue = 1L

Long newValue = oldValue + 1;          2个线程同时得到newValue = 2L

urlCounter.put(url, newValue);         2个线程先后put(url,2L),所以有一个线程相当于没做操作，所以结果少了。

 

 

都说concurrentHashMap是个线程安全的并发容器，所以没有显示加同步，实际效果呢并不如所愿。

问题就出在increase方法，concurrentHashMap能保证的是每一个操作（put，get,delete…）本身是线程安全的，但是我们的increase方法，

对concurrentHashMap的操作是一个组合，先get再put，所以多个线程的操作出现了覆盖。如果对整个increase方法加锁，那么又违背了我们使用并发容器的初衷，因为锁的开销很大。我们有没有方法改善统计方法呢？

 

 

方法1.AtomicLong

public class TestConcurrent {

​    private final static Map<String, AtomicLong> urlCounter = new ConcurrentHashMap<String, AtomicLong>();

 

​    // 接口调用次数+1

​    public void increase(String url) {

​        AtomicLong oldValue = urlCounter.get(url);

​        oldValue.getAndIncrement();

​        urlCounter.put(url, oldValue);

​    }

 

​    // 获取调用次数

​    public AtomicLong getCount(String url) {

​        return urlCounter.get(url);

​    }

 

​    public static void main(String[] args) {

​        ExecutorService executor = Executors.newFixedThreadPool(10);

​        final TestConcurrent counterDemo = new TestConcurrent();

​        int callTime = 1000;

​        final String url = "[http://localhost:8080/hello";](http://localhost:8080/hello)

​        AtomicLong al = new AtomicLong(0L);

​        urlCounter.put(url, al);

​        final CountDownLatch countDownLatch = new CountDownLatch(callTime);

​        // 模拟并发情况下的接口调用统计

​        for (int i = 0; i < callTime; i++) {

​            executor.execute(new Runnable() {

​                @Override

​                public void run() {

​                    counterDemo.increase(url);

​                    countDownLatch.countDown();

​                }

​            });

​        }

​        try {

​            countDownLatch.await();

​        } catch (InterruptedException e) {

​            e.printStackTrace();

​        }

​        executor.shutdown();

​        // 等待所有线程统计完成后输出调用次数

​        System.out.println("调用次数：" + counterDemo.getCount(url).get());

​    }

}

 

调用次数：1000

AtomicLong：

public final long getAndIncrement() {

​    while (true) {

​        long current = get();

​        long next = current + 1;

​        if (compareAndSet(current, next))

​            return current;

​    }

}

 

方法2.

concurrentHashMap父接口concurrentMap的一个非常有用但是又常常被忽略的方法。

/**

\* Replaces the entry for a key only if currently mapped to a given value.

\* This is equivalent to

\*  <pre> {@code

\* if (map.containsKey(key) && Objects.equals(map.get(key), oldValue)) {         ！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！

\*   map.put(key, newValue);

\*   return true;

\* } else

\*   return false;

\* }</pre>

*

\* except that the action is performed atomically.

*/

boolean replace(K key, V oldValue, V newValue);

 

 

/**

​     \* If the specified key is not already associated

​     \* with a value, associate it with the given value.

​     \* This is equivalent to

​     \*  <pre> {@code

​     \* if (!map.containsKey(key))

​     \*   return map.put(key, value);

​     \* else

​     \*   return map.get(key);

​     \* }</pre>

​     *

​     \* except that the action is performed atomically.

​     */

​     V putIfAbsent(K key, V value);

 

这其实就是一个最典型的CAS操作，except that the action is performed atomically.这句话真是帮了大忙，我们可以保证比较和设置是一个原子操作，当A线程尝试在increase时，旧值被修改的话就回导致replace失效，而我们只需要用一个循环，不断获取最新值，直到成功replace一次，即可完成统计。

 

public class TestConcurrent {

​    private final Map<String, Long> urlCounter = new ConcurrentHashMap<String, Long>();

​    

​    //接口调用次数+1

​    public long increase(String url) {

​        Long oldValue, newValue;

​        while (true) {

​            oldValue = urlCounter.get(url);

​            if (oldValue == null) {

​                newValue = 1l;

​                //初始化成功，退出循环

​                if (urlCounter.putIfAbsent(url, 1l) == null)

​                    break;

​                //如果初始化失败，说明其他线程已经初始化过了

​            } else {

​                newValue = oldValue + 1;

​                //+1成功，退出循环

​                if (urlCounter.replace(url, oldValue, newValue))

​                    break;

​                //如果+1失败，说明其他线程已经修改过了旧值

​            }

​        }

​        return newValue;

​    }

​    //获取调用次数

​    public Long getCount(String url){

​        return urlCounter.get(url);

​    }

​    public static void main(String[] args) {

​        ExecutorService executor = Executors.newFixedThreadPool(10);

​        final TestConcurrent counterDemo = new TestConcurrent();

​        int callTime = 1000;

​        final String url = "[http://localhost:8080/hello";](http://localhost:8080/hello)

​        final CountDownLatch countDownLatch = new CountDownLatch(callTime);

​        //模拟并发情况下的接口调用统计

​        for(int i=0;i<callTime;i++){

​            executor.execute(new Runnable() {

​                @Override

​                public void run() {

​                    counterDemo.increase(url);

​                    countDownLatch.countDown();

​                }

​            });

​        }

​        try {

​            countDownLatch.await();

​        } catch (InterruptedException e) {

​            e.printStackTrace();

​        }

​        executor.shutdown();

​        //等待所有线程统计完成后输出调用次数

​        System.out.println("调用次数："+counterDemo.getCount(url));

​    }

}

 

调用次数：1000

 

 

 

都说concurrentHashMap是个线程安全的并发容器，所以没有显示加同步，实际效果呢并不如所愿。问题就出在increase方法，concurrentHashMap能保证的是每一个操作（put，get,delete…）本身是线程安全的。

都说concurrentHashMap是个线程安全的并发容器，所以没有显示加同步，实际效果呢并不如所愿。问题就出在increase方法，concurrentHashMap能保证的是每一个操作（put，get,delete…）本身是线程安全的。

都说concurrentHashMap是个线程安全的并发容器，所以没有显示加同步，实际效果呢并不如所愿。问题就出在increase方法，concurrentHashMap能保证的是每一个操作（put，get,delete…）本身是线程安全的。

都说concurrentHashMap是个线程安全的并发容器，所以没有显示加同步，实际效果呢并不如所愿。问题就出在increase方法，concurrentHashMap能保证的是每一个操作（put，get,delete…）本身是线程安全的。

都说concurrentHashMap是个线程安全的并发容器，所以没有显示加同步，实际效果呢并不如所愿。问题就出在increase方法，concurrentHashMap能保证的是每一个操作（put，get,delete…）本身是线程安全的。

 

 

 

CAS操作的缺陷：

1.

CAS操作容易导致ABA问题,也就是在做a++之间，a可能被多个线程修改过了，只不过回到了最初的值，这时CAS会认为a的值没有变。a在外面 逛了一圈回来，你能保证它没有做任何坏事，不能！！也许它讨闲，把b的值减了一下，把c的值加了一下等等，更有甚者如果a是一个对象，这个对象有可能是新 创建出来的，a是一个引用呢情况又如何，所以这里面还是存在着很多问题的，解决ABA问题的方法有很多，可以考虑增加一个修改计数，只有修改计数不变的且 a值不变的情况下才做a++，也可以考虑引入版本号，当版本号相同时才做a++操作等，这和事务原子性处理有点类似！

 

 

因为CAS需要在操作值的时候检查下值有没有发生变化，如果没有发生变化则更新，但是如果一个值原来是A，变成了B，又变成了A，那么使用CAS进行检查时会发现它的值没有发生变化，但是实际上却变化了。ABA问题的解决思路就是使用版本号。在变量前面追加上版本号，每次变量更新的时候把版本号加一，那么A－B－A 就会变成1A-2B－3A。

从Java1.5开始JDK的atomic包里提供了一个类AtomicStampedReference来解决ABA问题。这个类的compareAndSet方法作用是首先检查当前引用是否等于预期引用，并且当前标志是否等于预期标志，如果全部相等，则以原子方式将该引用和该标志的值设置为给定的更新值。

 

关于ABA问题参考文档: [http://blog.hesey.NET/2011/09/resolve-aba-by-atomicstampedreference.html](http://blog.hesey.net/2011/09/resolve-aba-by-atomicstampedreference.html)

 

 

\2. 循环时间长开销大。自旋CAS如果长时间不成功，会给CPU带来非常大的执行开销。如果JVM能支持处理器提供的pause指令那么效率会有一定的提升，pause指令有两个作用，第一它可以延迟流水线执行指令（de-pipeline）,使CPU不会消耗过多的执行资源，延迟的时间取决于具体实现的版本，在一些处理器上延迟时间是零。第二它可以避免在退出循环的时候因内存顺序冲突（memory order violation）而引起CPU流水线被清空（CPU pipeline flush），从而提高CPU的执行效率。

 

 

3.

只能保证一个共享变量的原子操作。当对一个共享变量执行操作时，我们可以使用循环CAS的方式来保证原子操作，但是对多个共享变量操作时，循环CAS就无法保证操作的原子性，这个时候就可以用锁，或者有一个取巧的办法，就是把多个共享变量合并成一个共享变量来操作。比如有两个共享变量i＝2,j=a，合并一下ij=2a，然后用CAS来操作ij。从Java1.5开始JDK提供了AtomicReference类来保证引用对象之间的原子性，你可以把多个变量放在一个对象里来进行CAS操作。

 

 

！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！

自己的理解：

a++：

在操作a+时，先获取要操作的a到一个临时变量temp，增加操作 就 作用于 temp， 操作完temp之后， 判断 当前a == temp，如果相等，则再把 a 覆盖为 操作完之后的temp，否则回旋

 

当多个线程同时使用CAS操作一个变量时，只有一个会胜出，并成功更新，其余均会失败。失败的线程不会被挂起，仅是被告知失败，并且允许再次尝试，当然也允许失败的线程放弃操作。

 

！！！！！！！！！！！！！！！！！ 临时变量  临时变量  临时变量  临时变量

！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！

 

=======================================================================AtomicReference=======================================================================

AtomicReference和AtomicInteger非常类似，不同之处就在于AtomicInteger是对整数的封装，而AtomicReference则对应普通的对象引用。也就是它可以保证你在修改对象引用时的线程安全性

 

之前我们说过，线程判断被修改对象是否可以正确写入的条件是对象的当前值和期望是否一致。这个逻辑从一般意义上来说是正确的。但有可能出现一个小小的例外，就是当你获得对象当前数据后，在准备修改为新值前，对象的值被其他线程连续修改了2次，而经过这2次修改后，对象的值又恢复为旧值。这样，当前线程就无法正确判断这个对象究竟是否被修改过。ABA问题。

 

一般来说，发生这种情况的概率很小。而且即使发生了，可能也不是什么大问题。比如，我们只是简单得要做一个数值加法，即使在我取得期望值后，这个数字被不断的修改，只要它最终改回了我的期望值，我的加法计算就不会出错。也就是说，当你修改的对象没有过程的状态信息，所有的信息都只保存于对象的数值本身。

 

但是，在现实中，还可能存在另外一种场景。就是我们是否能修改对象的值，不仅取决于当前值，还和对象的过程变化有关，这时，AtomicReference就无能为力了。

现在，我们就来模拟这个场景，为了演示AtomicReference，我在这里使用AtomicReference实现这个功能。首先，我们模拟用户账户余额。

定义用户账户余额：

static AtomicReference<Integer> money=new AtomicReference<Integer>();

// 设置账户初始值小于20，显然这是一个需要被充值的账户

money.set(19);

 

接着，我们需要若干个后台线程，它们不断扫描数据，并为满足条件的客户充值。

public void test(){

​     //模拟多个线程同时更新后台数据库，为用户充值

​     for(int i = 0 ; i < 3 ; i++) {            

​         new Thread(){

​             public void run() {

​                while(true){

​                    while(true){

​                        Integer m=money.get();

​                        if(m<20){

​                            if(money.compareAndSet(m, m+20)){

​                      System.out.println("余额小于20元，充值成功，余额:"+money.get()+"元");

​                                 break;

​                            }

​                    }else{

​                            //System.out.println("余额大于20元，无需充值");

​                             break ;

​                        }

​                     }

​                 }

​             }

​         }.start();

​     }

}

 

上述代码第8行，判断用户余额并给予赠予金额。如果已经被其他用户处理，那么当前线程就会失败。因此，可以确保用户只会被充值一次。

此时，如果很不幸的，用户正好正在进行消费，就在赠予金额到账的同时，他进行了一次消费，使得总金额又小于20元，并且正好累计消费了20元。使得消费、赠予后的金额等于消费前、赠予前的金额。这时，后台的赠予进程就会误以为这个账户还没有赠予，所以，存在被多次赠予的可能。下面，模拟了这个消费线程：

 

public void test(){

​     //用户消费线程，模拟消费行为

​     new Thread() {

​         public voidrun() {

​             for(inti=0;i<100;i++){

​                while(true){

​                    Integer m=money.get();

​                     if(m>10){

​                        System.out.println("大于10元");

​                        if(money.compareAndSet(m, m-10)){

​                            System.out.println("成功消费10元，余额:"+money.get());

​                            break;

​                        }

​                    }else{

​                        System.out.println("没有足够的金额");

​                        break;

​                     }

​                 }

​                 try{Thread.sleep(100);} catch (InterruptedException e) {}

​             }

​         }

​     }.start();

}

 

上述代码中，消费者只要贵宾卡里的钱大于10元，就会立即进行一次10元的消费。执行上述程序，得到的输出如下：

余额小于20元，充值成功，余额:39元

大于10元

成功消费10元，余额:29

大于10元

成功消费10元，余额:19

余额小于20元，充值成功，余额:39元

大于10元

成功消费10元，余额:29

大于10元

成功消费10元，余额:39

余额小于20元，充值成功，余额:39元

从这一段输出中，可以看到，这个账户被先后反复多次充值。其原因正是因为账户余额被反复修改，修改后的值等于原有的数值。使得CAS操作无法正确判断当前数据状态。

虽然说这种情况出现的概率不大，但是依然是有可能的出现的。因此，当业务上确实可能出现这种情况时，我们也必须多加防范。体贴的JDK也已经为我们考虑到了这种情况，使用AtomicStampedReference就可以很好的解决这个问题。

 

 

 

AtomicReference介绍和函数列表

// 使用 null 初始值创建新的 AtomicReference。

AtomicReference()

// 使用给定的初始值创建新的 AtomicReference。

AtomicReference(V initialValue)

 

// 如果当前值 == 预期值，则以原子方式将该值设置为给定的更新值。

boolean compareAndSet(V expect, V update)

// 获取当前值。

V get()

// 以原子方式设置为给定值，并返回旧值。

V getAndSet(V newValue)

// 最终设置为给定值。

void lazySet(V newValue)

// 设置为给定值。

void set(V newValue)

// 返回当前值的字符串表示形式。

String toString()

// 如果当前值 == 预期值，则以原子方式将该值设置为给定的更新值。

boolean weakCompareAndSet(V expect, V update)

 

 

public class Person {

​    volatile long id;

​    public Person(long id) {

​        this.id = id;

​    }

​    public String toString() {

​        return "id:"+id;

​    }

}

public static void main(String[] args) {

​    // 创建两个Person对象，它们的id分别是101和102。

​    Person p1 = new Person(101);

​    Person p2 = new Person(102);

​    // 新建AtomicReference对象，初始化它的值为p1对象

​    AtomicReference ar = new AtomicReference(p1);

​    // 通过CAS设置ar。如果ar的值为p1的话，则将其设置为p2。

​    ar.compareAndSet(p1, p2);

 

​    Person p3 = (Person)ar.get();

​    System.out.println("p3 is "+p3);

​    System.out.println("p3.equals(p1)="+p3.equals(p1));

​    System.out.println("p3.equals(p2)="+p3.equals(p2));

}

结果：

p3 is id:102

p3.equals(p1)=false

p3.equals(p2)=true

 

 

 

public class Test

{

​    public final static AtomicReference<String> atomicString = new AtomicReference<String>("hosee");

​    public static void main(String[] args)

​    {

​        for (int i = 0; i < 10; i++)

​        {

​            final int num = i;

​            new Thread() {

​                public void run() {

​                    try

​                    {

​                        Thread.sleep(Math.abs((int)Math.random()*100));

​                    }

​                    catch (Exception e)

​                    {

​                        e.printStackTrace();

​                    }

​                    if (atomicString.compareAndSet("hosee", "ztk"))

​                    {

​                        System.out.println(Thread.currentThread().getId() + "Change value");

​                    }else {

​                        System.out.println(Thread.currentThread().getId() + "Failed");

​                    }

​                };

​            }.start();

​        }

​    }

}

10Failed

13Failed

9Change value

11Failed

12Failed

15Failed

17Failed

14Failed

16Failed

18Failed

 

=======================================================================用 AtomicStampedReference 解决ABA问题=======================================================================

各种乐观锁的实现中通常都会用版本戳version来对记录或对象标记，避免并发操作带来的问题，在Java中，AtomicStampedReference<E>也实现了这个作用，它通过包装[E,Integer]的元组来对对象标记版本戳stamp，从而避免ABA问题

例如下面的代码分别用AtomicInteger和AtomicStampedReference来对初始值为100的原子整型变量进行更新，AtomicInteger会成功执行CAS操作，而加上版本戳的AtomicStampedReference对于ABA问题会执行CAS失败：

 

public class ABA {

​    private static AtomicInteger atomicInt = new AtomicInteger(100);

​    private static AtomicStampedReference atomicStampedRef = new AtomicStampedReference(100, 0);

 

​    public static void main(String[] args) throws InterruptedException {

​            Thread intT1 = new Thread(new Runnable() {

​                    @Override

​                    public void run() {

​                            atomicInt.compareAndSet(100, 101);

​                            atomicInt.compareAndSet(101, 100);

​                    }

​            });

 

​            Thread intT2 = new Thread(new Runnable() {

​                    @Override

​                    public void run() {

​                            try {

​                                    TimeUnit.SECONDS.sleep(1);

​                            } catch (InterruptedException e) {

​                            }

​                            boolean c3 = atomicInt.compareAndSet(100, 101);

​                            System.out.println(c3); // true

​                    }

​            });

 

​            intT1.start();

​            intT2.start();

​            intT1.join();

​            intT2.join();

 

​            Thread refT1 = new Thread(new Runnable() {

​                    @Override

​                    public void run() {

​                            try {

​                                    TimeUnit.SECONDS.sleep(1);

​                            } catch (InterruptedException e) {

​                            }

​                            atomicStampedRef.compareAndSet(100, 101, atomicStampedRef.getStamp(), atomicStampedRef.getStamp() + 1);

​                            atomicStampedRef.compareAndSet(101, 100, atomicStampedRef.getStamp(), atomicStampedRef.getStamp() + 1);

​                    }

​            });

 

​            Thread refT2 = new Thread(new Runnable() {

​                    @Override

​                    public void run() {

​                            int stamp = atomicStampedRef.getStamp();

​                            try {

​                                    TimeUnit.SECONDS.sleep(2);

​                            } catch (InterruptedException e) {

​                            }

​                            boolean c3 = atomicStampedRef.compareAndSet(100, 101, stamp, stamp + 1);

​                            System.out.println(c3); // false

​                    }

​            });

 

​            refT1.start();

​            refT2.start();

​    }

}

 

AtomicStampedReference的几个API在AtomicReference的基础上新增了有关时间戳的信息：

//比较设置 参数依次为：期望值 写入新值 期望时间戳 新时间戳

public boolean compareAndSet(V expectedReference,V  

newReference,int expectedStamp,int newStamp)

//获得当前对象引用

public V getReference()

//获得当前时间戳

public int getStamp()

//设置当前对象引用和时间戳

public void set(V newReference, int newStamp)

 

 

01 public class AtomicStampedReferenceDemo {

02 static AtomicStampedReference<Integer> money=new AtomicStampedReference<Integer>(19,0);

03    public staticvoid main(String[] args) {

04        //模拟多个线程同时更新后台数据库，为用户充值

05        for(int i = 0 ; i < 3 ; i++) {

06            final int timestamp=money.getStamp();

07             newThread() {  

08                public void run() {

09                    while(true){

10                        while(true){

11                             Integerm=money.getReference();

12                             if(m<20){

13                          if(money.compareAndSet(m,m+20,timestamp,timestamp+1)){

14           System.out.println("余额小于20元，充值成功，余额:"+money.getReference()+"元");

15                                     break;

16                                 }

17                             }else{

18                                //System.out.println("余额大于20元，无需充值");

19                                 break ;

20                             }

21                        }

22                    }

23                }

24            }.start();

25         }

26        

27        //用户消费线程，模拟消费行为

28        new Thread() {

29             publicvoid run() {

30                for(int i=0;i<100;i++){

31                    while(true){

32                        int timestamp=money.getStamp();

33                        Integer m=money.getReference();

34                        if(m>10){

35                             System.out.println("大于10元");

36                          if(money.compareAndSet(m, m-10,timestamp,timestamp+1)){

37                       System.out.println("成功消费10元，余额:"+money.getReference());

38                                 break;

39                             }

40                        }else{

41                            System.out.println("没有足够的金额");

42                             break;

43                        }

44                    }

45                    try {Thread.sleep(100);} catch (InterruptedException e) {}

46                 }

47             }

48        }.start();

49    }

50 }

 

 

 

余额小于20元，充值成功，余额:39元

大于10元

成功消费10元，余额:29

大于10元

成功消费10元，余额:19

大于10元

成功消费10元，余额:9

没有足够的金额

可以看到，账户只被赠予了一次。

 

 

=======================================================================================红黑树=======================================================================================

https://www.cnblogs.com/CarpenterLee/p/5503882.html

 

 

​    

========================================================================上传文件 SpringMVC:用MultipartFile上传单个文件,多个文件======================================================

https://blog.csdn.net/u014746965/article/details/78772896

 

 

========================================================================文件路径========================================================================

1、

①直接是使用  String relativelyPath=System.getProperty("user.dir");

 

2.

第二种方式：使用当前类的类加载器进行获取 ClassLoader

首先来回顾一下，如何获取Class字节码实例，三种方式：（比如我的类叫Demo）

① Demo.class

② Class.forName("类的全称")

③ 利用Demo的实例对象，调用对象的getClass()方法获取该对象的Class实例

 

回顾了如何获取Class字节码实例之后，然后再来回顾一下，如何获取ClassLoader对象

① Demo.class.getClassLoader()

② Class.forName("类的全称").getClassLoader()

③ 假设demo为Demo的实例化对象 demo.getClass().getClassLoader()

④ 通过Thread对象的getContextClassLoader() 方法来获取

Thread.currentThread().getContextClassLoader()

① 依然是使用 ClassLoader, 其中有两个方法，两者一个是静态一个非静态

ClassLoader.getSystemResourceAsStream("config/log4j.properties");

Thread.currentThread().getContextClassLoader().getResourceAsStream("config/log4j.properties");

 

3.

② 先通过File文件包装之后，然后新建一个输入流

File file01 = new File("config/log4j.properties");

System.out.println(file01.getAbsolutePath());

 

File file02 = new File(properties.getProperty("user.dir") + "/bin/config/log4j.properties");

System.out.println(file02.getAbsolutePath());

 

//ClassLoader.getSystemResource获取的是URL对象

File file03 = new File(ClassLoader.getSystemResource("config/log4j.properties").getPath());

System.out.println(file03.getAbsolutePath());

 

其中创建file03 的方式不建议采纳，因为getSystemResource方法如果没获取到文件，则得到的

 

URL对象为null，此时再调用getPath()就会报错

 

 

 

相对路径：

所谓相对路径：指的是相对于整个web应用在硬盘上的路径来说的

web应用都是发布到tomcat的webapps下面执行的

 

说说Java文件读取的机制了：

如果你直接这样写路径new File("a.txt");那么tomcat就会从程序启动的地方去找这个文件（Java项目中也是如此），

那么web应用是从有tomcat来执行的，，tomcat这个程序是从哪里启动的呢？？答对了，就是tomcat/bin/startuo.bat启动的。

所以：

File f = new File("1.txt");

 

那么怎么找?

servlet中用ServlertContext域的getRealPath()这个方法找

对于ServletContext().getRealPath("路径名A");这个方法，无论你的路径名A是什么，ServletContext().getRealPath()方法底层都会在路径名A前拼上当前web应用的硬盘路径，，这样加上你传进去的路径就可以找成功找到了

其实通过ServletContext().getRealPath来拼接路径只是绝对硬盘路径的升级版，，，但是它好久好在计时你的web应用换了服务器环境，只要你的文件在web应用的中的相对路径不变，那么不论你的web应用如何更换服务器环境，都能动态的获取当前服务器环境的绝对文件路径。

当然，上面的getRealPath()方法只能在servlet中使用（因为只有servlet才有ServletContext域对象）

 

如果只是普通的java类，那么你也可以直接使用绝对硬盘路径，，但同样，服务器环境换了之后就可能会挂掉。可以通过类加载器ClassLoader类的getResource()方法来加载文件。。原理是：

类加载器是从你的web应用的WEB-INF\class文件夹下找.class文件来加载的。所以呢，你要找的web应用中的文件只要相对于你的class文件夹找就可以了。

 

其实类加载器也是搞出来一个绝对硬盘路径来找文件的，只是这个绝对路径是随着web应用的路径变化而变化的，就不存在web应用换了服务器环境找不到资源的问题了

 

 

 

 

 

https://www.cnblogs.com/Buffalo-L/p/4468483.html

 

 

========================================================================Spring Data + Thymeleaf 3 + Bootstrap 4 实现 分页器========================================================================

 

http://www.importnew.com/24722.html

 

 

========================================================================jQuery分页 插件 --pagination========================================================================

 

 

 

========================================================================JAVA8 Stream========================================================================

http://www.importnew.com/24237.html

 

http://www.importnew.com/24235.html

 

 

========================================================================更好的使用JAVA线程池========================================================================

ThreadPoolExecutor提供了很多可以配置的参数和可被用来扩展的钩子。

 

使用Executors#newCachedThreadPool可以快速创建一个拥有自动回收线程功能且没有限制的线程池。

使用Executors#newFixedThreadPool可以用来创建一个固定线程大小的线程池。

使用Executors#newSingleThreadExecutor可以用来创建一个单线程的执行器。

executor.setRejectedExecutionHandler(new ThreadPoolExecutor.DiscardPolicy());

 

利用Hook嵌入你的行为:

ThreadPoolExecutor提供了protected类型可以被覆盖的钩子方法，允许用户在任务执行之前会执行之后做一些事情。

我们可以通过它来实现比如初始化ThreadLocal、收集统计信息、如记录日志等操作。这类Hook如beforeExecute和afterExecute。

另外还有一个Hook可以用来在任务被执行完的时候让用户插入逻辑，如rerminated。

除此之外，你也可以通过实现 RejectedExecutionHandler 接口来编写自己的策略。下面是一个例子： 

ThreadPoolExecutor executor = new ThreadPoolExecutor(3, 6, 1, TimeUnit.SECONDS, queue, 

new RejectedExecutionHandler() { 

​    public void rejectedExecution(Runnable r, ThreadPoolExecutor executor) { 

​       System.out.println(String.format("Task %d rejected.", r.hashCode())); 

​    } 

}) 

 

 

 

========================================================================死循环问题的定位一般都是通过jps+jstack查看堆栈信息来定位的========================================================================

 

 

========================================================================jvm========================================================================

http://www.importnew.com/23742.html

 

 

========================================================================适配器模式========================================================================

适配器扮演着同样的角色：将一个接口转换成另一个接口，以符合客户的期望。\

 

假设已有一个软件系统，你希望它能和一个新的产商类库搭配使用，但是这个新产商所设计出来的接口，不同于旧产商的接口：

你不想改变现有的代码，解决这个问题（而且你也不能改变产商的代码）。所以该怎么做？你可以写一个类，将新产商接口转换成你所期望的接口。

这个适配器工作起来就如同一个中间人，它将客户所发出的请求转换成产商类能理解的请求。这个适配器实现了你的类所期望的接口，而且这个适配器也能和产商的接口沟通。

 

========================================================================迭代器模式========================================================================

关于迭代器模式，你所需要知道的第一件事情，就是它依赖于一个名为迭代器的接口

public interface Iterator {

​    // hasNext()方法返回一个布尔值，让我们知道是否还有更多的元素

​    boolean hasNext();

​    // next()方法返回下一个元素

​    Object next();

}

 

现在我们需要实现一个具体的迭代器，为餐厅菜单服务：

public class DinnerMenuIterator implements Iterator {

​    MenuItem[] items;

​    int position = 0;

​    public DinnerMenuIterator(MenuItem[] items) {

​        this.items = items;

​    }

​    public Object next() {

​        MenuItem menuItem = items[position];

​        position = position + 1;

​        return menuItem;

​    }

​    public boolean hasNext() {

​        if (position >= items.length || items[position] == null) {

​            return false;

​        } else {

​            return true;

​        }

​    }

​    // 我们需要实现remove()方法。因为使用的是固定长度的数组，

​    // 所以在remove()方法被调用时，我们将后面的所有元素往前移动一个位置。

​    @Override

​    public void remove() {

​        if (position <= 0) {

​            throw new IllegalStateException("You can't remove

​             an item until you've done at least one next()");

​        }

​        if (items[position - 1] != null) {

​            for (int i = position-1; i < (items.length - 1); i++) {

​                items[i] = items[i + 1];

​            }

​            items[items.length - 1] = null;

​        }

​    }

}

 

 

=======================================================================================UUID=======================================================================================

jdk1.5出了UUID这个类来生成唯一的字符串标识

 

UUID含义是通用唯一识别码 (Universally Unique Identifier),这是一个软件建构的标准,也是被开源软件基金会(Open Software Foundation, OSF)的组织应用在分布式计算环境(Distributed Computing Environment, DCE)领域的重要部分

 

UUID 的目的是让分布式系统中的所有元素，都能有唯一的辨识资讯，而不需要透过中央控制端来做辨识资讯的指定。

如此一来，每个人都可以建立不与其它人冲突的 UUID。在这样的情况下，就不需考虑数据库建立时的名称重复问题。

目前最广泛应用的 UUID，即是微软的 Microsoft's Globally Unique Identifiers (GUIDs)，而其他重要的应用，

则有 Linux ext2/ext3 档案系统、LUKS 加密分割区、GNOME、KDE、Mac OS X 等等。

 

UUID是指在一台机器上生成的数字，它保证对在同一时空中的所有机器都是唯一的。通常平台会提供生成的API。

按照开放软件基金会(OSF)制定的标准计算，用到了以太网卡地址、纳秒级时间、芯片ID码和许多可能的数字

UUID由以下几部分的组合：

（1）当前日期和时间，UUID的第一个部分与时间有关，如果你在生成一个UUID之后，过几秒又生成一个UUID，则第一个部分不同，其余相同。

（2）时钟序列。

（3）全局唯一的IEEE机器识别号，如果有网卡，从网卡MAC地址获得，没有网卡以其他方式获得。

UUID的唯一缺陷在于生成的结果串会比较长。关于UUID这个标准使用最普遍的是微软的GUID(Globals Unique Identifiers)。

在ColdFusion中可以用CreateUUID()函数很简单地生成UUID，其格式为：xxxxxxxx-xxxx- xxxx-xxxxxxxxxxxxxxxx(8-4-4-16)，

其中每个 x 是 0-9 或 a-f 范围内的一个十六进制的数字。而标准的UUID格式为：

xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (8-4-4-4-12)，可以从cflib 下载CreateGUID() UDF进行转换。

 

使用UUID的好处在分布式的软件系统中（比如：DCE/RPC, COM+,CORBA）就能体现出来，

它能保证每个节点所生成的标识都不会重复，并且随着WEB服务等整合技术的发展，UUID的优势将更加明显。根据使用的特定机制，UUID不仅需要保证是彼此不相同的，或者最少也是

与公元3400年之前其他任何生成的通用唯一标识符有非常大的区别。UUID最少在3000+年内不会重复。

 

生成UUID：

String aw = LBIUUID.getUUID();

System.out.println(aw);

结果：

87e1a0f8493741cf805c64a7a6c3c46f

 

 

=======================================================================================排序 算法 5亿整数的大文件，怎么排？=======================================================================================

http://www.importnew.com/23450.html

 

 

=======================================================================================大数据日志  日交易额百亿级交易系统的超轻量日志实现=======================================================================================

http://www.importnew.com/23206.html

 

https://github.com/cyfonly/FLogger

 

http://www.cnblogs.com/cyfonly/p/6139049.html

 

！！！！！！！！！！！！！！！！！！！！！！！！！！

双缓冲队列的思想。

在每次写日志时，日志内容作为一个 StringBuffer 添加到当前正在使用的 ArrayList<StringBuffer> 中，另一个则空闲。当内存中的日志输出到磁盘文件时，会将当前使用的 ArrayList<StringBuffer> 与空闲的 ArrayList<StringBuffer> 进行角色交换，交换后之前空闲的 ArrayList<StringBuffer> 将接收日志内容，而之前拥有日志内容的 ArrayList<StringBuffer> 则用来输出日志到磁盘文件。这样就可以避免每次刷盘时影响日志内容的接收（即所谓的 stop-the-world 效应）及多线程问题。

 

日志接收代码：

//同步单个文件的日志

synchronized(lfi){

　　　　if(lfi.currLogBuff == 'A'){

　　　　　　　　lfi.alLogBufA.add(logMsg);

　　　　}else{

　　　　　　　　lfi.alLogBufB.add(logMsg);

　　　　}

　　　　lfi.currCacheSize += CommUtil.StringToBytes(logMsg.toString()).length;

}

 

 

日志刷盘代码：

//获得需要进行输出的缓存列表

ArrayList<StringBuffer> alWrtLog = null;

synchronized(lfi){

　　　　if(lfi.currLogBuff == 'A'){

　　　　　　　　alWrtLog = lfi.alLogBufA;

　　　　　　　　lfi.currLogBuff = 'B';

　　　　}else{

　　　　　　　　alWrtLog = lfi.alLogBufB;

　　　　　　　　lfi.currLogBuff = 'A';

　　　　}

　　　　lfi.currCacheSize = 0;

}

//创建日志文件

createLogFile(lfi);

//输出日志

int iWriteSize = writeToFile(lfi.fullLogFileName,alWrtLog);

lfi.currLogSize += iWriteSize;

 

 

往A中写日志，currLogBuff == 'A'，释放lfi， 刷盘日志了，alWrtLog = 'A',从A中写到磁盘，currLogBuff = 'B'，释放锁，进行IO操作。写日志了，currLogBuff = 'B'，存到B中，如之前A进行IO没有冲突

 

 

=======================================================================================页面缓存=======================================================================================

http://www.importnew.com/23131.html

 

https://www.cnblogs.com/belove8013/p/8134067.html

 

前端页面缓存心得体会：

都有哪些缓存？

缓存包括客户端缓存(浏览器缓存)和服务器缓存，一般我们说的都是浏览器缓存，缓存就是把访问后的动态文件生成一份静态文件的备份，当用户再次请求时，直接获取静态文件，极大减少服务器压力。

 

怎么控制缓存？

通过在页面的head中添加no-cache和expiration等信息，即可控制浏览器不缓存页面，例如下面的代码

<meta http-equiv="pragma"
content="no-cache">

<meta http-equiv="Cache-Control"
content="no-cache, must-revalidate">

<meta http-equiv="expires"
content="Wed, 26 Feb 1997 08:21:57 GMT">

 

这里的304代表加载缓存资源，200代表加载的服务器最新资源

 

 

=======================================================================================DateTimeFormatter=======================================================================================

SimpleDateFormat不能在多线程环境下使用，这个很基础的问题！！JDK1.8提供了DateTimeFormatter类支持并发，可以替代。

 

 

 

 

=======================================================================================Spring8：一些常用的Spring Bean扩展接口=======================================================================================

InitializingBean 、DisposableBean

 

这两个接口是一组的，功能类似，因此放在一起：前者顾名思义在Bean属性都设置完毕后调用afterPropertiesSet()方法做一些初始化的工作，后者在Bean生命周期结束前调用destory()方法做一些收尾工作。

InitializingBean接口、Disposable接口可以和init-method、destory-method配合使用，接口执行顺序优先于配置

InitializingBean接口、Disposable接口底层使用类型强转.方法名()进行直接方法调用，init-method、destory-method底层使用反射

afterPropertiesSet()方法是在Bean的属性设置之后才会进行调用，某个Bean的afterPropertiesSet()方法执行完毕才会执行下一个Bean的afterPropertiesSet()方法，因此不建议在afterPropertiesSet()方法中写处理时间太长的方法

 

 

BeanNameAware、ApplicationContextAware和BeanFactoryAware

 

这三个接口放在一起写，是因为它们是一组的，作用相似。

“Aware”的意思是”感知到的”，那么这三个接口的意思也不难理解：

1、实现BeanNameAware接口的Bean，在Bean加载的过程中可以获取到该Bean的id

2、实现ApplicationContextAware接口的Bean，在Bean加载的过程中可以获取到Spring的ApplicationContext，这个尤其重要，ApplicationContext是Spring应用上下文，从ApplicationContext中可以获取包括任意的Bean在内的大量Spring容器内容和信息

3、实现BeanFactoryAware接口的Bean，在Bean加载的过程中可以获取到加载该Bean的BeanFactory

 

看一下例子：

public class AwareBean implements BeanNameAware, BeanFactoryAware, ApplicationContextAware

{

​    private String                     beanName;

​    private ApplicationContext        applicationContext;

​    private BeanFactory                beanFactory;

​    public void setBeanName(String beanName)

​    {

​        System.out.println("Enter AwareBean.setBeanName(), beanName = " + beanName + "\n");

​        this.beanName = beanName;

​    }

​    public void setApplicationContext(ApplicationContext applicationContext) throws BeansException

​    {

​        System.out.println("Enter AwareBean.setApplicationContext(), applicationContext = " + applicationContext + "\n");

​        this.applicationContext = applicationContext;

​    }

​    public void setBeanFactory(BeanFactory beanFactory) throws BeansException

​    {

​        System.out.println("Enter AwareBean.setBeanFactory(), beanfactory = " + beanFactory + "\n");

​        this.beanFactory = beanFactory;

​    }

}

 

<bean id="AwareBean" class="org.xrq.bean.aware.AwareBean" />

 

 

执行结果为：

Enter AwareBean.setBeanName(), beanName = AwareBean

Enter AwareBean.setBeanFactory(), beanfactory = org.springframework.beans.factory.support.DefaultListableBeanFactory@2747fda0: defining beans [AwareBean,org.springframework.context.annotation.internalConfigurationAnnotationProcessor,org.springframework.context.annotation.internalAutowiredAnnotationProcessor,org.springframework.context.annotation.internalRequiredAnnotationProcessor,org.springframework.context.annotation.internalCommonAnnotationProcessor,org.springframework.context.annotation.ConfigurationClassPostProcessor.importAwareProcessor,org.springframework.context.annotation.ConfigurationClassPostProcessor.enhancedConfigurationProcessor]; root of factory hierarchy

Enter AwareBean.setApplicationContext(), applicationContext = org.springframework.context.support.GenericApplicationContext@5514cd80: startup date [Mon Aug 08 19:23:30 CST 2016]; root of context hierarchy

 

 

 

 

FactoryBean

开发者除了设置Bean相关属性之外，是没有太多的自主权的。FactoryBean改变了这一点，开发者可以个性化地定制自己想要实例化出来的Bean，方法就是实现FactoryBean接口。

 

http://www.importnew.com/22775.html

 

=======================================================================================Java 钩子=======================================================================================

利用模板方法模式来说明钩子方法是什么

 

模板方法模式：在一个方法中定义一个算法的骨架，而将一些步骤延迟到子类中。模板方法使得子类可以在不改变算法结构的情况下，重新定义算法中的某些步骤。

 

【钩子方法】：原理就是实现为空的方法，在某任务之前、之后、执行中、报异常后调用的方法（是不是有种熟悉的感觉）。

通常钩子方法是通过抽象类或是本类中的空方法来实现的。

 

 

abstract class Client{

​    /**

​     \* 【模板方法】

​     */

​    public void templateMethod(){

​        before();

​        appetite();

​        after();

​    }

​    /**

​     \* 【钩子方法】在盛饭前（一个空的实现）

​     */

​     protected void before(){};

​    /**

​     \* 【抽象方法】告诉服务员其饭量

​     \* @return 饭量

​     */

​    public abstract void appetite();

​    /**

​     \* 【具体方法】盛饭后

​     */

​    private void after(){

​        //实际项目这里是共有的业务逻辑

​        System.out.println("拿筷子，找桌子，开吃...");

​    }

}

/**

*食堂

*/

class Restaurant{

​    /**

​     \* 打饭方法，前提是客户要告知服务员你的饭量，他会根据你的饭量给你“盛”饭

​     \* @param client 排队的客户

​     \* @return

​     */

​    public void dozenRice(Client client){

​        client.templateMethod();

​    }

}

public class Test1 { //业务处理类，老王去打饭

​    public static void main(String[] args) {

​        Restaurant waiter=new Restaurant();

​        waiter.dozenRice(new Client(){

​            @Override

​            protected void before() {

​                System.out.println("对服务员吹胡子瞪眼！！");

​            }

​            @Override

​            public void appetite() {

​                System.out.println("盛了一锅米饭");

​            }});

​    }

}

 

 

 

 

Runtime.getRuntime().addShutdownHook(shutdownHook);

这个方法的含义说明： 这个方法的意思就是在jvm中增加一个关闭的钩子，当jvm关闭的时候，会执行系统中已经设置的所有通过方法addShutdownHook添加的钩子，当系统执行完这些钩子后，jvm才会关闭。所以这些钩子可以在jvm关闭的时候进行内存清理、对象销毁等操作。

 

public class TestShutdownHook {

 /**

  \* @param args

  */

 public static void main(String[] args) {

  // 定义线程1

  Thread thread1 = new Thread() {

   public void run() {

​    System.out.println("thread1...");

   }

  };

  // 定义线程2

  Thread thread2 = new Thread() {

   public void run() {

​    System.out.println("thread2...");

   }

  };

  // 定义关闭线程

  Thread shutdownThread = new Thread() {

   public void run() {

​    System.out.println("shutdownThread...");

   }

  };

  // jvm关闭的时候先执行该线程钩子

  Runtime.getRuntime().addShutdownHook(shutdownThread);

  thread1.start();

  thread2.start();

 }

}

 

打印结果：

thread2...

thread1...

shutdownThread...

 

或者：

thread2...

thread1...

shutdownThread...

 

结论：

无论是先打印thread1还是thread2，shutdownThread 线程都是最后执行的（因为这个线程是在jvm执行关闭前才会执行）。

 

 

=======================================================================================Java意义重大的7个性能指标=======================================================================================

响应时间和吞吐量：

吞吐量是指单位时间内系统处理的客户请求的数量。

 

 

 

=======================================================================================关于使用sql语句sum(case when……）来实现分类汇总功能=======================================================================================

 

比如有一张表有这样四个字段：月份、销售人员、销售数量、产品单价。

 

你是要按月分和销售人员来对销售额透视，而sql语句只对月份分组，正确结果应该增加分组维度

 

select

月份,

sum (case when 销售人员='姓名1' then 销售数量*产品单价 else 0 end) as 姓名1销售额,

sum (case when 销售人员='姓名2' then 销售数量*产品单价 else 0 end) as 姓名2销售额,

sum (case when 销售人员='姓名3' then 销售数量*产品单价 else 0 end) as 姓名3销售额

from 表格

group by 月份,销售人员

 

1月 姓名1 1 100

1月 姓名1 2 300

1月 姓名2 2 400

2月 姓名2 2 400

 

聚合函数 一定是先分组，再聚合。  如果不先 group by，就相当于把所有的数据当成一组。

 

 

=======================================================================================thrift=======================================================================================

简单来说,是Facebook公布的一款开源跨语言的RPC框架.

 

 

https://www.cnblogs.com/fingerboy/p/6424248.html

 

http://www.importnew.com/23211.html

 

 

 

=======================================================================================ehcache实现页面整体缓存和页面局部缓存=======================================================================================

http://www.importnew.com/23131.html

 

https://blog.csdn.net/huwei2003/article/details/76343781

 

 

 

=======================================================================================java7 TransferQueue=======================================================================================

public interface TransferQueue<E> extends BlockingQueue<E>

 

public class LinkedTransferQueue<E> extends AbstractQueue<E>

​    implements TransferQueue<E>, java.io.Serializable

 

之前的BlockingQueue是对 读取 或者 写入 锁定整个队列，所以在比较繁忙的时候，各种锁比较耗时

​    public void put(E e) throws InterruptedException {

​        checkNotNull(e);

​        final ReentrantLock lock = this.lock;

​        lock.lockInterruptibly();

​        try {

​            while (count == items.length)

​                notFull.await();

​            insert(e);

​        } finally {

​            lock.unlock();

​        }

​    }

而当时有一个SynchronizedQueue其实不能叫Queue，因为只能放一个物件，要么有一个物件在等人拿，要么有一个空等人放

根据这个原理，诞生了LinkedTransferQueue，利用CompareAndSwap进行一个无界阻塞的队列，针对每一个操作进行处理样大家就不用抢得那么辛苦了

 

存：

put();   放元素进去队列，注意队列是可以无限长的

add();   同上

transfer();  这个是重点，如果队列中有人发现有人在等，则直接给那个人（有一个参数waiter指定了在等的线程）

如果没人在等，就放进队列

 

取：

poll();  立即返回，如果没有元素就是空

take(); 如果没有元素，那就等

 

 

BlockingQueue（和Queue）是Java 5中加入的接口，它是指这样的一个队列：当生产者向队列添加元素但队列已满时，生产者会被阻塞；当消费者从队列移除元素但队列为空时，消费者会被阻塞。

 

TransferQueue则更进一步，生产者会一直阻塞直到所添加到队列的元素被某一个消费者所消费（不仅仅是添加到队列里就完事）。新添加的transfer方法用来实现这种约束。顾名思义，阻塞就是发生在元素从一个线程transfer到另一个线程的过程中，它有效地实现了元素在线程之间的传递

 

TransferQueue还包括了其他的一些方法：两个tryTransfer方法，一个是非阻塞的，另一个带有timeout参数设置超时时间的。还有两个辅助方法hasWaitingConsumer()和getWaitingConsumerCount()。

 

 

当我第一次看到TransferQueue时，首先想到了已有的实现类SynchronousQueue。SynchronousQueue的队列长度为0，最初我认为这好像没多大用处，但后来我发现它是整个Java Collection Framework中最有用的队列实现类之一，特别是对于两个线程之间传递元素这种用例。

 

TransferQueue相比SynchronousQueue用处更广、更好用，因为你可以决定是使用BlockingQueue的方法（译者注：例如put方法）还是确保一次传递完成（译者注：即transfer方法）。在队列中已有元素的情况下，调用transfer方法，可以确保队列中被传递元素之前的所有元素都能被处理。Doug Lea说从功能角度来讲，LinkedTransferQueue实际上是ConcurrentLinkedQueue、SynchronousQueue（公平模式）和LinkedBlockingQueue的超集。而且LinkedTransferQueue更好用，因为它不仅仅综合了这几个类的功能，同时也提供了更高效的实现。

 

 

性能测试的结果 TransferQueue表明它优于Java 5的那些类（译者注：ConcurrentLinkedQueue、SynchronousQueue和LinkedBlockingQueue）。

 

LinkedTransferQueue的性能分别是SynchronousQueue的3倍（非公平模式）和14倍（公平模式）。因为像ThreadPoolExecutor这样的类在任务传递时都是使用SynchronousQueue，所以使用LinkedTransferQueue来代替SynchronousQueue也会使得ThreadPoolExecutor得到相应的性能提升。

 

Java 5中的SynchronousQueue使用两个队列（一个用于正在等待的生产者、另一个用于正在等待的消费者）和一个用来保护两个队列的锁。而LinkedTransferQueue使用CAS操作（译者注：参考wiki）实现一个非阻塞的方法，这是避免序列化处理任务的关键

 

TransferQueue   可以代替 ConcurrentLinkedQueue、SynchronousQueue（公平模式）和LinkedBlockingQueue ？

 

 

有一个使用案例，我们知道 ThreadPoolExecutor 调节线程的原则是：先调整到最小线程，最小线程用完后，他会将优先将任务放入缓存队列 (offer(task)), 等缓冲队列用完了，才会向最大线程数调节。这似乎与我们所理解的线程池模型有点不同。我们一般采用增加到最大线程后，才会放入缓冲队列中，以达到最大性能。 ThreadPoolExecutor 代码段：

如果我们采用 SynchronousQueue 作为 ThreadPoolExecuto 的缓冲队列时，在没有线程执行 poll 时 ( 即存在等待线程 ) ，则 workQueue.offer(command) 返回 false, 这时 ThreadPoolExecutor就会增加线程，最快地达到最大线程数。但也仅此而已，也因为 SynchronousQueue 本身不存在容量 , 也决定了我们一般无法采用 SynchronousQueue 作为 ThreadPoolExecutor 的缓存队列。而一般采用 LinkedBlockingQueue 的 offer 方法来实现。最新的 LinkedTransferQueue 也许可以帮我们解决这个问题，后面再说。

transfer 算法比较复杂，实现很难看明白。大致的理解是采用所谓双重数据结构 (dual data structures) 。之所以叫双重，其原因是方法都是通过两个步骤完成：

 

保留与完成。比如消费者线程从一个队列中取元素，发现队列为空，他就生成一个空元素放入队列 , 所谓空元素就是数据项字段为空。然后消费者线程在这个字段上旅转等待。这叫保留。直到一个生产者线程意欲向队例中放入一个元素，这里他发现最前面的元素的数据项字段为 NULL，他就直接把自已数据填充到这个元素中，即完成了元素的传送。大体是这个意思，这种方式优美了完成了线程之间的高效协作。

 

 

PaddedAtomicReference 相对于父类 AtomicReference 只做了一件事情，就将共享变量追加到64 字节。我们可以来计算下，一个对象的引用占 4 个字节，

它追加了 15 个变量共占 60 个字节，再加上父类的 Value 变量，一共 64 个字节。 上面追加15个4字节对象的代码看起来是不是很奇葩？其实不是的 , 这样做是为了在并发中提升效率。

为什么追加 64 字节能够提高并发编程的效率呢 ？ 因为对于英特尔酷睿 i7 ，酷睿， Atom 和 NetBurst ， Core Solo 和

PentiumM处理器的 L1 ， L2 或 L3 缓存的高速缓存行是 64 个字节宽，不支持部分填充缓存行，这意味着如果队列的头节点和尾节点都不足 64 字节的话，处理器会将它们都读到同一个高速缓存行中，在多处理器下每个处理器都会缓存同样的头尾节点，当一个处理器试图修改头接点时会将整个缓存行锁定，那么在缓存一致性机制的作用下，会导致其他处理器不能访问自己高速缓存中的尾节点，而队列的入队和出队操作是需要不停修改头接点和尾节点，所以在多处理器的情况下将会严重影响到队列的入队和出队效率。 Doug lea 使用追加到 64 字节的方式来填满高速缓冲区的缓存行，避免头接点和尾节点加载到同一个缓存行，使得头尾节点在修改时不会互相锁定。

 

那么是不是在使用 Volatile 变量时都应该追加到 64 字节呢？不是的。在两种场景下不应该使用这种方式。第一： 缓存行非 64 字节宽的处理器 ，如 P6 系列和奔腾处理器，它们的 L1 和 L2 高速缓存行是 32 个字节宽。第二： 共享变量不会被频繁的写 。因为使用追加字节的方式需要处理器读取更多的字节到高速缓冲区，这本身就会带来一定的性能消耗，共享变量如果不被频繁写的话，锁的几率也非常小，就没必要通过追加字节的方式来避免相互锁定。

 

 

===================================================ConcurrentLinkedQueue 、 SynchronousQueue 、 BlockingQueue 、 TransferQueue 、 LinkedTransferQueue===========================================================

TransferQueue ：

public interface TransferQueue<E> extends BlockingQueue<E> {

​    1.tryTransfer(E)：将元素立刻给消费者。准确的说就是立刻给一个等待接收元素的线程，如果没有消费者就会返回false，而不将元素放入队列。

 

　　2.transfer(E)：将元素给消费者，如果没有消费者就会等待。生产者会一直阻塞直到所添加到队列的元素被某一个消费者所消费（不仅仅是添加到队列里就完事）。

 

　　3.tryTransfer(E,long,TimeUnit)：将元素立刻给消费者，如果没有就等待指定时间。给失败返回false。

 

　　4.hasWaitingConsumer()：返回当前是否有消费者在等待元素。

 

　　5.getWaitingConsumerCount()：返回等待元素的消费者个数

}

transfer会阻塞，tryTransfer不会阻塞

LinkedTransferQueue ：

https://blog.csdn.net/qq_38293564/article/details/80593821

LinkedTransferQueue是一个由链表结构组成的 无界 阻塞 TransferQueue队列。相对于其他阻塞队列，LinkedTransferQueue多了tryTransfer和transfer方法。

 

LinkedTransferQueue只有两个构造方法，这里不再详细介绍：

public LinkedTransferQueue() { }

public LinkedTransferQueue(Collection<? extends E> c) {

​    this();

​    addAll(c);

}

 

由于队列的实现，其需要遍历队列才能计算出队列的大小(isEmpty)，这期间队列发生的改变，遍历的结果会不正确。bulk操作并不保证原子性，比如迭代器迭代的时候执行addAll()方法，迭代器可能只能看到部分新加的元素。

 

通常阻塞队里中，生产者放入元素，消费者使用元素，这两个部分是分离的。这里的分离意思如下：厨师做好了菜放在柜台上，服务员端走，厨师是不需要管有没有人取走做的菜，服务员也不需要管厨师有没有做好菜，没做好菜阻塞就行了。上面就是个人所说的分离的意思。TransferQueue接口定义的相关内容就是厨师会知道做好的菜有没有被取走。

 

使用场景

当我们不想生产者过度生产消息时，TransferQueue可能非常有用，可避免发生OutOfMemory错误。在这样的设计中，消费者的消费能力将决定生产者产生消息的速度。

 

实例：

public class LinkedTransferQueueDemo {

​    static LinkedTransferQueue<String> lnkTransQueue = new LinkedTransferQueue<String>();

​    public static void main(String[] args) {

​        ExecutorService exService = Executors.newFixedThreadPool(2);

​        Producer producer = new LinkedTransferQueueDemo().new Producer();

​        Consumer consumer = new LinkedTransferQueueDemo().new Consumer();

​        exService.execute(producer);

​        exService.execute(consumer);

​        exService.shutdown();

​    }

​    class Producer implements Runnable{

​        @Override

​        public void run() {

​            for(int i=0;i<3;i++){

​                try {

​                    System.out.println("Producer is waiting to transfer...");

​                    lnkTransQueue.transfer("A"+i);

​                    System.out.println("producer transfered element: A"+i);

​                } catch (InterruptedException e) {

​                    e.printStackTrace();

​                }

​            }

​        }

​    }

​    class Consumer implements Runnable{

​        @Override

​        public void run() {

​            for(int i=0;i<3;i++){

​                try {

​                    System.out.println("Consumer is waiting to take element...");

​                    String s= lnkTransQueue.take();

​                    System.out.println("Consumer received Element: "+s);

​                } catch (InterruptedException e) {

​                    e.printStackTrace();

​                }

​            }

​        }

​    }

}

 

 

 

Producer is waiting to transfer...

Consumer is waiting to take element...

producer transfered element: A0

Producer is waiting to transfer...

Consumer received Element: A0

Consumer is waiting to take element...

producer transfered element: A1

Producer is waiting to transfer...

Consumer received Element: A1

Consumer is waiting to take element...

Consumer received Element: A2

producer transfered element: A2

 

===================================================LinkedTransferQueue字节追加提高并发度技术，ConcurrentHaspMap结合volatile的happen-before读取优化===================================================

 

 

 

 

===================================================Happens-before 规则======================================================================================================

JMM中一个重要问题就是：如何让多线程之间，对象的状态对于各线程的“可视性”是顺序一致的。

它的解决方式就是 Happens-before 规则：JVM为所有程序内部动作定义了一个偏序关系，叫做happens-before。要想保证执行动作B的线程看到动作A的结果（无论A和B是否发生在同一个线程中），A和B之间就必须满足happens-before关系。

 

我们现在来看一下“Happens-before”规则都有哪些（摘自《Java并发编程实践》）：

　　① 程序次序法则：线程中的每个动作A都happens-before于该线程中的每一个动作B，其中，在程序中，所有的动作B都能出现在A之后。

　　② 监视器锁法则：对一个监视器锁的解锁 happens-before于每一个后续对同一监视器锁的加锁。

　　③ volatile变量法则：对volatile域的写入操作happens-before于每一个后续对同一个域的读写操作。

　　④ 线程启动法则：在一个线程里，对Thread.start的调用会happens-before于每个启动线程的动作。

　　⑤ 线程终结法则：线程中的任何动作都happens-before于其他线程检测到这个线程已经终结、或者从Thread.join调用中成功返回，或Thread.isAlive返回false。

　　⑥ 中断法则：一个线程调用另一个线程的interrupt happens-before于被中断的线程发现中断。

　　⑦ 终结法则：一个对象的构造函数的结束happens-before于这个对象finalizer的开始。

　　⑧ 传递性：如果A happens-before于B，且B happens-before于C，则A happens-before于C

 

 

https://blog.csdn.net/oChangWen/article/details/77824692

 

 

 

===================================================web.xml 组件加载顺序======================================================================================================

web.xml组件加载顺序为：context-param -> listener -> filter -> servlet(同类则按编写顺序执行)。

 

 

 

 

===================================================关于ajax的拦截器，ajax超时处理======================================================================================================

 

 

 

 

 

===================================================HandlerExceptionResolver  全局捕获异常的功能 会捕获没catch住的异常 你可以自己抛出一个不捕获的异常测试一下是否成功======================================================================================================

继承HandlerExceptionResolver自定义异常处理器：

 

package com.orange.exception;

public class NameException extends Exception {

​    public NameException() {

​        super();

​    }

​    public NameException(String message) {

​        super(message);

​    }

}

 

 

package com.orange.exception;

public class PasswordException extends Exception {

​    public PasswordException() {

​        super();

​    }

​    public PasswordException(String message) {

​        super(message);

​    }  

}

 

public class MyExceptionResolver implements HandlerExceptionResolver {

​    @Override

​    public ModelAndView resolveException(HttpServletRequest request, HttpServletResponse response, Object handler,

​            Exception ex) {

​        ModelAndView mav = new ModelAndView();

​        mav.addObject("ex", ex);

​        mav.setViewName("/defaultException.jsp");

​        

​        if(ex instanceof NameException){

​            mav.setViewName("/showException.jsp");

​        }

​        

​        if(ex instanceof PasswordException){

​            mav.setViewName("/showException.jsp");

​        }

​        

​        return mav;

​    }

}

 

 

首先描述实现的功能：因为在项目中，我们不可否认的会出现异常，而且这些异常并没有进行捕获。经常出现的bug如空指针异常等等。

在之前的项目中，如果我们没有进行任何配置，那么容器会自动打印错误的信息，如果tomcat的404页面，400页面等等。

如果我们在web.xml中进行如下配置，就会拦截错误，然后跳转到指定的错误页面。

<error-page>

​    <error-code>500</error-code>

​    <location>/500.jsp</location>

</error-page>

但是这已经落后了，现在我们通过实现spring的HandlerExceptionResolver接口来捕获所有的异常。

 

 

 

如何实现：

1、新建GlobalExceptionResolver如下

/**

\* 全局异常捕获

\* @author XXX

*/

public class GlobalExceptionResolver implements HandlerExceptionResolver{

 

​    @Override

​    public ModelAndView resolveException(HttpServletRequest request, HttpServletResponse response, Object handler,

​            Exception exception) {

​        //--------------------------------------------

​        return null;

​    }

}

 

2、在spring配置文件中配置刚才新建的类

<bean class="com.ssm.exception.GlobalExceptionResolver" />

 

3、根据自己的需求修改GlobalExceptionResolver的横线部分

在你在开发的时候，请返回null，这样这个类就如同不起作用，之前该怎么样就怎么样。

当开发完成之后，根据错误的信息来返回需要的东西了。

首先我们可以做的是打印错误日志，当然也是必须的。

System.err.println("访问" + request.getRequestURI() + " 发生错误, 错误信息:" + exception.getMessage());

这里我只是用控制台举例，你当然可以用日志框架打印。打印信息主要是包括是访问那个地址出现了什么错误。

之后如果你需要返回错误页面，那么就直接在ModelAndView里面写就行了，这里就不多举例了，ModelAndView写过MVC的Controller应该都熟悉。

 

ModelAndView modelAndView = new ModelAndView();

modelAndView.setViewName("error");

return modelAndView;

 

 

注意：

1、注意不同类型和来源的请求。

因为在实际项目中，可能遇到各种请求类型，如正常的get，post。也可能是来自ajax的请求。

所以如果均返回同一个ModelAndView显然可能有点不合适，对于ajax可能需要特别处理。

还有就是如果有手机端和PC在同一个项目中的情况，那么来源不同，返回的页面也可能不同。虽然可以交给前端去做自适应处理，但是我们还是得做好考虑。

总之，要考虑到各种不同的请求，单一返回可能并不适用所有项目。

 

 

 

 

全局异常spring有2套：

1、HandlerExceptionResolver接口及其实现

2、@ExceptionHandler 配合 ControllerAdvice使用，这一套是需要第1种方法中提供的ExceptionHandlerExceptionResolver实现来处理的。

这些个东西，HandlerExceptionResolver是接口，ExceptionHandlerExceptionResolver是其实现，ExceptionHandler 是注解，名字看起来很像，不深入研究源代码，很容易被搞晕。

而楼主也说了spring推荐的是第二套，至于为什么，可能是第1套是在DispacherServlet里的配置，而spring不希望业务开发者配多了这些东西，把DispacherServlet里的配置搞得乱七八糟然后把自己搞晕。

 

 

我现在已经使用的是【@ExceptionHandler 配合 @ControllerAdvice使用】的模式了。

从实际表现来看，有下面几个优点：

1、使用注解的方式代码看上去更加的清晰。

2、对于自定义异常的捕获会很方便。

3、适用于对于返回json格式的情况（可以使用@ResponseBody注解方法对特定异常进行处理），使用HandlerExceptionResolver的话如果是ajax的请求，出现异常就会很尴尬，ajax并不认识ModelAndView。

 

 

如果是ajax请求，出现异常，可以以下面的方法返回错误信息：

MappingJackson2JsonView view = new MappingJackson2JsonView();

view.setObjectMapper(jacksonObjectMapper);

view.setContentType("text/html;charset=UTF-8");

return new ModelAndView(view, map);

 

 

 

经过实践,找到一种便于理解的方式, 就是实现ErrorController接口 其他什么注解都不要

@RequestMapping(produces = "text/html;charset=UTF-8", consumes="text/html")

public ModelAndView errorHtml(HttpServletRequest request, HttpServletResponse response) {

​    Map<String, Object> model = getError(request, false);

​    return new ModelAndView("/error", model);

}

 

@RequestMapping(consumes= {"application/json","*/*"})

@ResponseBody

public ResponseEntity<Map<String, Object>> error(HttpServletRequest request) {

​    Map<String, Object> model = getError(request, true);

​    return new ResponseEntity<Map<String, Object>>(model, (HttpStatus)model.remove("status"));

}

通过produces 和, consumes来区分客户端要的是html还是json, getError里面用instanceOf区分各种异常,不用@ExceptionHandler去注解各种类型的异常处理

这要求前端的访问必须严谨的设置accept头来告诉服务器你到底需要的是什么.

这样的好处是我可以在一个类里面就看到全局异常处理的所有面貌, 不用再乱七八糟找了.

缺点就是instanceOf区分各种异常的代码有点长, 不过我们一般只处理业务逻辑异常和权限异常,其他异常统统作为"开发或运维前必须解决的异常"来兜底处理, 所以这段代码仍然是可以理解的.

 

 

 

 

SpringMVC HandlerExceptionResolver踩坑记:

如果我们要自定义异常解析器，如统一返回json格式的异常信息给客户端，那我们就需要自定义HandlerExceptionResolver。

之前是实现的接口HandlerExceptionResolver，来处理ServiceException和内部错误，后来想处理参数绑定异常BindException，但死活不成功。

原因在于，SpringMVC默认有多个异常解析器，DefaultHandlerExceptionResolver就是其中一个，而且它处理了BindException；同时，更为重要的是，（通过断点调试发现）它的顺序在自定义异常解析器之前，而org.springframework.web.servlet.DispatcherServlet#processHandlerException中是按照这些解析器的顺序来处理异常的，一旦前面的解析器处理产生结果，后面的将不再执行：

for (HandlerExceptionResolver handlerExceptionResolver : this.handlerExceptionResolvers) {

​            exMv = handlerExceptionResolver.resolveException(request, response, handler, ex);

​            if (exMv != null) {

​                break;

​            }

}

 

 

解决：把自定义的RestHandlerExceptionResolver顺序调前：

public class RestHandlerExceptionResolver extends AbstractHandlerExceptionResolver {

...省略其他代码

  // 解析器顺序，越小发挥作用越早

public int getOrder() {

​    return 0;

  }

}

 

 

 

 

===================================================DispatcherServlet======================================================================================================

https://www.cnblogs.com/tengyunhao/p/7518481.html

在整个 Spring MVC 框架中，DispatcherServlet 处于核心位置，它负责协调和组织不同组件完成请求处理并返回响应工作。在看 DispatcherServlet 类之前，我们先来看一下请求处理的大致流程：

1.Tomcat 启动，对 DispatcherServlet 进行实例化，然后调用它的 init() 方法进行初始化，在这个初始化过程中完成了：

对 web.xml 中初始化参数的加载；建立 WebApplicationContext (SpringMVC的IOC容器)；进行组件的初始化；

2.客户端发出请求，由 Tomcat 接收到这个请求，如果匹配 DispatcherServlet 在 web.xml 中配置的映射路径，Tomcat 就将请求转交给 DispatcherServlet 处理；

3.DispatcherServlet 从容器中取出所有 HandlerMapping 实例（每个实例对应一个 HandlerMapping 接口的实现类）并遍历，每个 HandlerMapping 会根据请求信息，通过自己实现类中的方式去找到处理该请求的 Handler (执行程序，如Controller中的方法)，并且将这个 Handler 与一堆 HandlerInterceptor (拦截器) 封装成一个 HandlerExecutionChain 对象，一旦有一个 HandlerMapping 可以找到 Handler 则退出循环；（详情可以看 [Java]SpringMVC工作原理之二：HandlerMapping和HandlerAdpater 这篇文章）

4.DispatcherServlet 取出 HandlerAdapter 组件，根据已经找到的 Handler，再从所有 HandlerAdapter 中找到可以处理该 Handler 的 HandlerAdapter 对象；

5.执行 HandlerExecutionChain 中所有拦截器的 preHandler() 方法，然后再利用 HandlerAdapter 执行 Handler ，执行完成得到 ModelAndView，再依次调用拦截器的 postHandler() 方法；

6.利用 ViewResolver 将 ModelAndView 或是 Exception（可解析成 ModelAndView）解析成 View，然后 View 会调用 render() 方法再根据 ModelAndView 中的数据渲染出页面；

7.最后再依次调用拦截器的 afterCompletion() 方法，这一次请求就结束了。

 

 

HttpServlet 提供了 doGet()、doPost() 等方法，DispatcherServlet 中这些方法是在其父类 FrameworkServlet 中实现的，代码如下：

@Override

protected final void doGet(HttpServletRequest request, HttpServletResponse response)

​        throws ServletException, IOException {

​    processRequest(request, response);

}

@Override

protected final void doPost(HttpServletRequest request, HttpServletResponse response)

​        throws ServletException, IOException {

​    processRequest(request, response);

}

 

这些方法又都调用了 processRequest() 方法，我们来看一下代码：

protected final void processRequest(HttpServletRequest request, HttpServletResponse response)

​        throws ServletException, IOException {

​    long startTime = System.currentTimeMillis();

​    Throwable failureCause = null;

​    // 返回与当前线程相关联的 LocaleContext

​    LocaleContext previousLocaleContext = LocaleContextHolder.getLocaleContext();

​    // 根据请求构建 LocaleContext，公开请求的语言环境为当前语言环境

​    LocaleContext localeContext = buildLocaleContext(request);

​    

​    // 返回当前绑定到线程的 RequestAttributes

​    RequestAttributes previousAttributes = RequestContextHolder.getRequestAttributes();

​    // 根据请求构建ServletRequestAttributes

​    ServletRequestAttributes requestAttributes = buildRequestAttributes(request, response, previousAttributes);

​    

​    // 获取当前请求的 WebAsyncManager，如果没有找到则创建

​    WebAsyncManager asyncManager = WebAsyncUtils.getAsyncManager(request);    

​    asyncManager.registerCallableInterceptor(FrameworkServlet.class.getName(), new RequestBindingInterceptor());

 

​    // 使 LocaleContext 和 requestAttributes 关联

​    initContextHolders(request, localeContext, requestAttributes);

 

​    try {

​        // 由 DispatcherServlet 实现

​        doService(request, response);       //!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

​    } catch (ServletException ex) {

​    } catch (IOException ex) {

​    } catch (Throwable ex) {

​    } finally {

​        // 重置 LocaleContext 和 requestAttributes，解除关联

​        resetContextHolders(request, previousLocaleContext, previousAttributes);

​        if (requestAttributes != null) {

​            requestAttributes.requestCompleted();

​        }// 发布 ServletRequestHandlerEvent 事件

​        publishRequestHandledEvent(request, startTime, failureCause);

​    }

}

 

DispatcherServlet 的 doService() 方法主要是设置一些 request 属性，并调用 doDispatch() 方法进行请求分发处理，doDispatch() 方法的主要过程是通过 HandlerMapping 获取 Handler，再找到用于执行它的 HandlerAdapter，执行 Handler 后得到 ModelAndView ，ModelAndView 是连接“业务逻辑层”与“视图展示层”的桥梁，接下来就要通过 ModelAndView 获得 View，再通过它的 Model 对 View 进行渲染。doDispatch() 方法如下：

 

​    protected void doDispatch(HttpServletRequest request, HttpServletResponse response) throws Exception {

​        HttpServletRequest processedRequest = request;

​        HandlerExecutionChain mappedHandler = null;

​        int interceptorIndex = -1;

 

​        try {

​            ModelAndView mv;

​            boolean errorView = false;

 

​            try {

​                processedRequest = checkMultipart(request);

 

​                // Determine handler for the current request.

​                mappedHandler = getHandler(processedRequest, false);

​                if (mappedHandler == null || mappedHandler.getHandler() == null) {

​                    noHandlerFound(processedRequest, response);

​                    return;

​                }

 

​                // Determine handler adapter for the current request.

​                HandlerAdapter ha = getHandlerAdapter(mappedHandler.getHandler());

 

​                // Process last-modified header, if supported by the handler.

​                String method = request.getMethod();

​                boolean isGet = "GET".equals(method);

​                if (isGet || "HEAD".equals(method)) {

​                    long lastModified = ha.getLastModified(request, mappedHandler.getHandler());

​                    if (logger.isDebugEnabled()) {

​                        String requestUri = urlPathHelper.getRequestUri(request);

​                        logger.debug("Last-Modified value for [" + requestUri + "] is: " + lastModified);

​                    }

​                    if (new ServletWebRequest(request, response).checkNotModified(lastModified) && isGet) {

​                        return;

​                    }

​                }

 

​                // Apply preHandle methods of registered interceptors.

​                HandlerInterceptor[] interceptors = mappedHandler.getInterceptors();

​                if (interceptors != null) {

​                    for (int i = 0; i < interceptors.length; i++) {

​                        HandlerInterceptor interceptor = interceptors[i];

​                        if (!interceptor.preHandle(processedRequest, response, mappedHandler.getHandler())) {

​                            triggerAfterCompletion(mappedHandler, interceptorIndex, processedRequest, response, null);

​                            return;

​                        }

​                        interceptorIndex = i;

​                    }

​                }

 

​                // Actually invoke the handler.

​                mv = ha.handle(processedRequest, response, mappedHandler.getHandler());     //!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!反射

 

​                // Do we need view name translation?

​                if (mv != null && !mv.hasView()) {

​                    mv.setViewName(getDefaultViewName(request));

​                }

 

​                // Apply postHandle methods of registered interceptors.

​                if (interceptors != null) {

​                    for (int i = interceptors.length - 1; i >= 0; i--) {

​                        HandlerInterceptor interceptor = interceptors[i];

​                        interceptor.postHandle(processedRequest, response, mappedHandler.getHandler(), mv);

​                    }

​                }

​            }

​            catch (ModelAndViewDefiningException ex) {

​                logger.debug("ModelAndViewDefiningException encountered", ex);

​                mv = ex.getModelAndView();

​            }

​            catch (Exception ex) {

​                Object handler = (mappedHandler != null ? mappedHandler.getHandler() : null);

​                mv = processHandlerException(processedRequest, response, handler, ex);    //!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!，对于 拦截器、controller的抛出的异常进行处理

​                errorView = (mv != null);

​            }

 

​            // Did the handler return a view to render?

​            if (mv != null && !mv.wasCleared()) {

​                render(mv, processedRequest, response);

​                if (errorView) {

​                    WebUtils.clearErrorRequestAttributes(request);

​                }

​            }

​            else {

​                if (logger.isDebugEnabled()) {

​                    logger.debug("Null ModelAndView returned to DispatcherServlet with name '" + getServletName() +

​                            "': assuming HandlerAdapter completed request handling");

​                }

​            }

 

​            // Trigger after-completion for successful outcome.

​            triggerAfterCompletion(mappedHandler, interceptorIndex, processedRequest, response, null);

​        }

 

​        catch (Exception ex) {

​            // Trigger after-completion for thrown exception.

​            triggerAfterCompletion(mappedHandler, interceptorIndex, processedRequest, response, ex);

​            throw ex;

​        }

​        catch (Error err) {

​            ServletException ex = new NestedServletException("Handler processing failed", err);

​            // Trigger after-completion for thrown exception.

​            triggerAfterCompletion(mappedHandler, interceptorIndex, processedRequest, response, ex);

​            throw ex;

​        }

 

​        finally {

​            // Clean up any resources used by a multipart request.

​            if (processedRequest != request) {

​                cleanupMultipart(processedRequest);

​            }

​        }

​    }

 

 

mv = processHandlerException(processedRequest, response, handler, ex);          ==========================》

 

​    protected ModelAndView processHandlerException(HttpServletRequest request, HttpServletResponse response,

​            Object handler, Exception ex) throws Exception {

 

​        ModelAndView exMv = null;

​        for (HandlerExceptionResolver handlerExceptionResolver : this.handlerExceptionResolvers) {                     //===================》 initHandlerExceptionResolvers(context);     是在tomcat启动时执行的

​            exMv = handlerExceptionResolver.resolveException(request, response, handler, ex);

​            if (exMv != null) {

​                break;

​            }

​        }

​        if (exMv != null) {

​            if (exMv.isEmpty()) {

​                return null;

​            }

​            // We might still need view name translation for a plain error model...

​            if (!exMv.hasView()) {

​                exMv.setViewName(getDefaultViewName(request));

​            }

​            if (logger.isDebugEnabled()) {

​                logger.debug("Handler execution resulted in exception - forwarding to resolved error view: " + exMv, ex);

​            }

​            WebUtils.exposeErrorRequestAttributes(request, ex, getServletName());

​            return exMv;

​        }

 

​        throw ex;

​    }

 

 

​    private void initHandlerExceptionResolvers(ApplicationContext context) {

​        this.handlerExceptionResolvers = null;

 

​        if (this.detectAllHandlerExceptionResolvers) {

​            // Find all HandlerExceptionResolvers in the ApplicationContext, including ancestor contexts.

​            Map<String, HandlerExceptionResolver> matchingBeans = BeanFactoryUtils

​                    .beansOfTypeIncludingAncestors(context, HandlerExceptionResolver.class, true, false);

​            if (!matchingBeans.isEmpty()) {

​                this.handlerExceptionResolvers = new ArrayList<HandlerExceptionResolver>(matchingBeans.values());

​                // We keep HandlerExceptionResolvers in sorted order.

​                OrderComparator.sort(this.handlerExceptionResolvers);

​            }

​        }

​        else {

​            try {

​                HandlerExceptionResolver her =

​                        context.getBean(HANDLER_EXCEPTION_RESOLVER_BEAN_NAME, HandlerExceptionResolver.class);

​                this.handlerExceptionResolvers = Collections.singletonList(her);

​            }

​            catch (NoSuchBeanDefinitionException ex) {

​                // Ignore, no HandlerExceptionResolver is fine too.

​            }

​        }

 

​        // Ensure we have at least some HandlerExceptionResolvers, by registering

​        // default HandlerExceptionResolvers if no other resolvers are found.

​        if (this.handlerExceptionResolvers == null) {

​            this.handlerExceptionResolvers = getDefaultStrategies(context, HandlerExceptionResolver.class);

​            if (logger.isDebugEnabled()) {

​                logger.debug("No HandlerExceptionResolvers found in servlet '" + getServletName() + "': using default");

​            }

​        }

​    }

 

从容器中找    HandlerExceptionResolver   =============》  自定义的异常处理:   

public class DetailedHandlerExceptionResolver implements HandlerExceptionResolver {

 

<bean id="detailedHandlerExceptionResolver"

​    class="com.suning.lbi.exception.DetailedHandlerExceptionResolver">

</bean>

 

例如:SUNING

public class DetailedHandlerExceptionResolver implements HandlerExceptionResolver {

 

​    public static final String NAME_ERRORMSG = "errorMsg";

​    public static final String NAME_ERRORMSG_DESC = "msg";

​    public static final String HEADER_USER_AGENT = "user-agent";

​    public static final String HTTP_JSON_BACKNAME = "jsonalert";

 

​    public static final String HEADER_REFER = "referer";

 

​    public static final Integer NUM_50 = 50;

​    public static final Integer NUM_200 = 200;

​    public static final Integer NUM_500 = 500;

​    private Logger LOGGER = LoggerFactory.getLogger(getClass());

 

​    /**

​     \* 异常处理

​     */

​    public ModelAndView resolveException(HttpServletRequest request, HttpServletResponse response, Object handler,

​            Exception ex) {

​        

​        //不打印登陆超时的异常

​        if(!(ex instanceof LbiLoginTimeOutException)){

​            LOGGER.error("异常{}",ex);

​        }

​        // 1、json请求

​        if (("true".equals(request.getParameter(HTTP_JSON_BACKNAME)) && checkIsJsonRequest(request)) || "true".equals(request.getParameter("isAjax"))) {

​            // 1.1对应的action不存在org.springframework.jdbc.BadSqlGrammarException

​            if (ex instanceof NoSuchRequestHandlingMethodException) {

​                String msg = "对应的请求链接不存在";

​                responseJson(response, request, HttpServletResponse.SC_BAD_REQUEST, msg);

​            } else if (ex instanceof LbiIllegalException) {

​                // 1.2应用抛出的异常异常，返回json,并输出ex.getMessage()异常信息

​                String msg = "错误：" + ex.getMessage();

​                responseJson(response, request, HttpServletResponse.SC_INTERNAL_SERVER_ERROR, msg);

​            } else if (ex instanceof LbiLimitLowException) {

​                // 1.3应用抛出的权限异常，返回json,并输出权限不足信息

​                String msg = ex.getMessage();

​                responseJson(response, request, HttpServletResponse.SC_FORBIDDEN, msg);

​            } else if (ex instanceof LbiRuntimeException) {

​                String msg = ex.getMessage();

​                responseJson(response, request, HttpServletResponse.SC_FORBIDDEN, msg);

​            }else if (ex instanceof LbiLoginTimeOutException) {

​                response.setHeader("status", "timeout");

​                String msg = "您的登录状态超时,请刷新页面重新登录!";

​                responseJson(response, request, HttpServletResponse.SC_INTERNAL_SERVER_ERROR, msg);

 

​            }else if (ex instanceof DataAccessException) {

​                String msg = "数据库或SQL异常!";

​                responseJson(response, request, HttpServletResponse.SC_INTERNAL_SERVER_ERROR, msg);

​            }else{

​                responseJson(response, request, HttpServletResponse.SC_INTERNAL_SERVER_ERROR, ex.getMessage());

​            }

​            return null;

​        } else { // 2、非json请求

​            // 2.1对应的action不存在

​            if (ex instanceof NoSuchRequestHandlingMethodException) {

​                return new ModelAndView("/errors/404");

​            } else if (ex instanceof LbiIllegalException) { // 2.2应用抛出的异常异常，返回json,并输出ex.getMessage()异常信息

​                String msg = ExceptionUtils.getStackTrace(ex);

​                ModelMap modelMap = new ModelMap();

​                modelMap.put(NAME_ERRORMSG, msg);

​                return new ModelAndView("/errors/500", modelMap);

​            } else if (ex instanceof LbiRuntimeException) { // 应用抛出的异常异常，返回json,并输出ex.getMessage()异常信息

​                String exMsg = ExceptionUtils.getStackTrace(ex);

​                String msg = ex.getMessage();

​                ModelMap modelMap = new ModelMap();

​                modelMap.put(NAME_ERRORMSG, exMsg);

​                modelMap.put(NAME_ERRORMSG_DESC, msg);

​                return new ModelAndView("/errors/500", modelMap);

​                /*return new ModelAndView("redirect:/errors/500.action",modelMap);*/

​            } else if (ex instanceof LbiLimitLowException) { // 2.3 应用抛出的权限异常，返回json,并输出权限不足信息

​                ModelMap model = new ModelMap();

​                model.put("to", request.getRequestURL());

​                model.put(NAME_ERRORMSG, ExceptionUtils.getStackTrace(ex));

​                /*return new ModelAndView("errors/limitLow", model);*/

​                return new ModelAndView("/errors/500",model);

​            }

​            else if (ex instanceof LbiLoginTimeOutException) {

 

​                /*return new ModelAndView("errors/limitLow", model);*/

​                ModelAndView model = new ModelAndView("/errors/LoginTimeOut");

​                model.addObject(NAME_ERRORMSG,ExceptionUtils.getStackTrace(ex));

​                return model;

​            } else {

​                ModelAndView model = new ModelAndView("/errors/500");

​                model.addObject("to", request.getRequestURL());

​                model.addObject(NAME_ERRORMSG, ExceptionUtils.getStackTrace(ex));

​                /*return new ModelAndView("errors/limitLow", model);*/

​                return model;

​            }

 

​        }

 

​    }

 

​    /**

​     \* 获取异常的堆栈信息 功能描述: <br>

​     \* 〈功能详细描述〉

​     *

​     \* @param handler

​     \* @param ex

​     \* @return

​     \* @see [相关类/方法](可选)

​     \* @since [产品/模块版本](可选)

​     */

​    Map<String, String> getExMessage(Object handler, Exception ex) {

​        Map<String, String> params = new HashMap<String, String>();

​        params.put(NAME_ERRORMSG, ExceptionUtils.getMessage(ex));

​        return params;

​    }

 

​    /**

​     \* 检查请求页是否包含分页信息

​     *

​     \* @param request

​     \* @return

​     */

​    boolean checkIsIncludePage(HttpServletRequest request) {

​        if (null != request.getParameter("page") || null != request.getParameter("rows")) {

​            return true;

​        }

​        return false;

 

​    }

 

​    /**

​     \* 检测request对象中是否包含json请求，该请求一般来自于浏览器 功能描述: <br>

​     \* 〈功能详细描述〉

​     *

​     \* @param request

​     \* @return

​     \* @see [相关类/方法](可选)

​     \* @since [产品/模块版本](可选)

​     */

​    boolean checkIsJsonRequest(HttpServletRequest request) {

​        if (request.getHeader("x-requested-with") != null

​                && "XMLHttpRequest".equalsIgnoreCase(request.getHeader("x-requested-with"))) {

​            // 如果是ajax请求响应头会有，x-requested-with；

​            return true;

​        }

​        return false;

​    }

 

​    /**

​     \* 返回json数据给客户端 功能描述: <br>

​     \* 〈功能详细描述〉

​     *

​     \* @param response

​     \* @param request

​     \* @param status 返回给客户端参数的状态码 400 500等

​     \* @param msg

​     \* @see [相关类/方法](可选)

​     \* @since [产品/模块版本](可选)

​     */

​    @SuppressWarnings({ "rawtypes", "unchecked" })

​    void responseJson(HttpServletResponse response, HttpServletRequest request, int status, String msg) {

​        response.setContentType("text/html;charset=UTF-8");

​        JsonBean jsonBean = new JsonBean();

​        jsonBean.setResult(false);

​        jsonBean.setMessage(msg);

​        jsonBean.setMore("");

​        jsonBean.setStatus(status);

​        if (checkIsIncludePage(request)) {

​            PageBean page = new PageBean();

​            page.setCurrentPage(1);

​            page.setPageSize(PageNumberUtil.pageSize);

​            page.setDatas(new ArrayList<Map<String, Object>>(0));

​            page.setTotalCount(0);

​            page.setTotalPages(0);

​            jsonBean.setData(page);

​        }

​        JSONObject jsonObj = JSONObject.fromObject(jsonBean);

​        PrintWriter pw = null;

​        try {

​            pw = response.getWriter();

​        } catch (IOException e) {

​            LOGGER.error("IO异常，", e);

​        } finally {

​            if (null != pw) {

​                pw.write(jsonObj.toString());

​                pw.flush();

​                pw.close();

​            }

​        }

​    }

 

​    /**

​     \* 获取异常的信息 功能描述: <br>

​     \* 〈功能详细描述〉

​     *

​     \* @param request

​     \* @param ex

​     \* @return

​     \* @see [相关类/方法](可选)

​     \* @since [产品/模块版本](可选)

​     */

​    @SuppressWarnings("unchecked")

​    Map<String, Object> getExLog(HttpServletRequest request, Exception ex) {

​        Map<String, Object> map = new HashMap<String, Object>();

​        Object uriId = request.getAttribute("requestUrlId");

​        map.put("uriId", uriId);

​        String uri = request.getRequestURI();

​        map.put("uri", uri);

​        String userId = RequestUtil.getLoginUserId(request);

​        map.put("userId", userId);

​        String referUrl = request.getHeader(HEADER_REFER);

​        map.put("referUrl", referUrl);

​        String userAgent = request.getHeader(HEADER_USER_AGENT);

​        map.put("userAgent", userAgent);

​        Map<String, Object> params = request.getParameterMap();

​        String param = iteratorMap(params, request);

​        if (StringUtils.isEmpty(param)) {

​            map.put("params", "");

​        } else if (param.length() > NUM_200) {

​            map.put("params", param.substring(0, NUM_200));

​        } else {

​            map.put("params", param);

​        }

 

​        String ip = NetWorkUtil.getRemortIP(request);

​        map.put("IP", ip == null ? "" : ip);

​        String className = ex.getClass().getName();

​        map.put("className", className == null ? "" : className.substring(0, NUM_50));

​        String message = ex.getMessage();

​        if (message == null) {

​            map.put("message", "");

​        } else if (message.length() > NUM_500) {

​            map.put("message", message.substring(0, NUM_500));

​        } else {

​            map.put("message", message);

​        }

 

​        String stackTrace = getStackTrace(ex);

​        stackTrace = stackTrace.substring(0, stackTrace.length() > NUM_500 ? NUM_500 : stackTrace.length());

​        map.put("stackTrace", stackTrace);

 

​        return map;

 

​    }

 

​    /**

​     *

​     \* 功能描述: 打印异常堆栈信息

​     *

​     \* @param t

​     \* @return String

​     \* @see [相关类/方法](可选)

​     \* @since [产品/模块版本](可选)

​     */

​    public static String getStackTrace(Throwable t) {

​        StringWriter sw = new StringWriter();

​        PrintWriter pw = new PrintWriter(sw, true);

​        pw.flush();

​        sw.flush();

​        return sw.toString();

​    }

 

​    public static String iteratorMap(Map<String, Object> map, HttpServletRequest request) {

​        if (null == map) {

​            return "";

​        }

​        StringBuilder sbr = new StringBuilder("[");

​        Set<String> key = map.keySet();

​        for (@SuppressWarnings("rawtypes")

​        Iterator it = key.iterator(); it.hasNext();) {

​            String s = (String) it.next();

​            sbr.append(s).append(":").append(request.getParameter(s)).append(",");

​        }

​        sbr.append("]");

​        return sbr.toString();

 

​    }

 

}    

​    

 

所以：超时异常怎么做呢？

public class LoginInterceptor implements HandlerInterceptor {    

​    @Override

​    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {

 

​        String currentURL = request.getServletPath();

​        String ip = request.getRemoteAddr();

​        @SuppressWarnings("unchecked")

​        Map<String, Object> params = request.getParameterMap();

​        logger.info("url:{},ip:{}",currentURL,ip);

​        

​        /*Cookie[] cookie = (Cookie[]) request.getCookies();

​        Map<String, String> cookMap = new HashMap<String, String>();

​        for (int i = 0; i < cookie.length; i++) {

​            Cookie cook = cookie[i];

​            cookMap.put(cook.getName(),cook.getValue());

​        }

 

​        UserLoginBean ulBean = (UserLoginBean) request.getSession().getAttribute(LBIConstants.USER_KEY);      //通过获取session中的key 来判断要不要抛出 LbiLoginTimeOutException，如果抛出了，会被doDispacher方法捕获

​        if (ulBean == null) {

​            logger.info("未登陆,url:{},ip:{}",currentURL,ip);

​            throw new LbiLoginTimeOutException();

​        }else{

​            logger.info("url:{},ip:{},userid:{}",currentURL,ip,ulBean.getUserId());

​        }

 

​        String uri = request.getRequestURI();

 

​        //if (uri.endsWith("index.action") || uri.endsWith("manage.action")) {

​            String userId = ulBean.getUserId();

​            saveLog(userId, uri,params);

​        //}

 

​        return true;

​    }

}

​    

​    

那么问题来了：     UserLoginBean ulBean = (UserLoginBean) request.getSession().getAttribute("sesssion_user_key");   通过这个来判断是否超时，什么时候超时了，将其设置为null

​    /**

​     \* 登陆验证

​     */

​    @RequestMapping(value = "/initIndex.action")

​    public ModelAndView submit(HttpServletRequest request, HttpServletResponse response) {

 

​        ModelAndView mv = new ModelAndView();

​        Map<String, Object> params = this.getParams(request);

​       

​        

​        String userName = MapUtils.getString(params, "username");

​        String password = URLDecoder.decode(MapUtils.getString(params, "password",""));

​        String uuid = MapUtils.getString(params, "uuid","");

​        String verificode = MapUtils.getString(params, "verificode","");

 

​        /* String token = MapUtils.getString(params, "token","");

 

​        

​       if(!MD5.getMD5(MapUtils.getString(params, "IP")).equals(token)){

​            mv.setViewName("login");

​            mv.addObject("errorCode", "0001");

​            mv.addObject("token", MD5.getMD5(MapUtils.getString(params, "IP")));

​            mv.addObject("errorMessage", "");

​            return mv;

​        }*/

​        

​        String domain = request.getServerName();

​        //外网域名访问增加图像验证操作

​        if(domain.indexOf(".[suning.com](http://suning.com/)")>-1){

​            if(!ValidationService.validate(PropertyUtil.getProperty("vcs.domain")+"/vcs/validate.htm", uuid, verificode, "1")){

​                 mv.setViewName("login");

​                 mv.addObject("errorMessage", "验证码错误");

​                 isOutside(request,mv);

​                 return mv;

​            }

​        }

​        

​        if (StringUtils.isEmpty(userName) || StringUtils.isEmpty(password)) {

​            mv.setViewName("login");

​            //mv.addObject("token", MD5.getMD5(MapUtils.getString(params, "IP")));

​            mv.addObject("errorMessage", "用户名或者密码不能为空");

​            return mv;

​        }

 

​        // 20181217 18047093 检查 TSOR_EMP_AREA_D.EMP_NO

​        if(!userService.checkEmployeeId(userName)){

​            mv.setViewName("login");

​            mv.addObject("errorMessage", "用户没有权限");

​            return mv;

​        }

 

​        if (checkLogin(userName, password)) {

​            UserLoginBean ulBean = new UserLoginBean();

​            ulBean.setUserId(userName.toUpperCase());

​            ulBean.setUserName("");

​            ulBean.setSuning(true);

​            this.userService.queryDaquAndWerks(ulBean);            //！！！！！！！！！！！！！！！！！！！！！！！！该用户拥有的大区，物流中心权限。在登录时保存在session中

​            this.userService.queryUserFunction(userName, ulBean);

 

​            params.put("employeeid", userName);

​            String userType = this.commonService.queryObject("cardanalysis.queryAuth", params, String.class);

​            ulBean.setHq(HQ.equals(userType) ? true : false);

 

​            // 保存用户会话信息到session

​            HttpSession session = request.getSession();

​            session.setAttribute("sesssion_user_key", ulBean);                  //！！！！！！！！！！！！！！！！！！！！！！！！在登录系统时，给用户的session赋值了，

 

​            params.put("roleCode", getRoleCode());

​            List<Map<String, Object>> list = commonService.queryList("functionnew2.queryFuncAllByRole", params);

​            mv.addObject("menu", JSONObject.toJSON(list).toString());

​            mv.addObject("url","/lbi-web-in/main/toHome.action");

​            mv.setViewName("tianyanNew/index/index");

​            

​            //继续跳到老页面   

​            //saveUserLoginInfo(userName);

​            //return new ModelAndView("redirect:/main/toIndexNew.action?type=2&functinCode=TAB_03_01_01");

​            

​            

​            //获取首页快捷入库权限

​           /* String[] code={"jxkh",""};

​            List<String> codes = Arrays.asList(code);

​            params.put("codes", codes);

​            List<Map<String, Object>> codesList = this.commonService.queryList("functionnew2.queryFuncAllByRole", params);

​            mv.addObject("codesList", JSONObject.toJSON(codesList).toString());*/

​        } else {

​            mv.setViewName("login");

​            mv.addObject("errorCode", "0003");

​            mv.addObject("errorMessage", "用户名或者密码错误");

​            isOutside(request,mv);

​        }

​        //saveUserLoginInfo(userName);

​        return mv;

​    }

​    

​    

​    

​        /**

​     \* 注销

​     *

​     \* @param request

​     \* @param response

​     \* @return

​     */

​    @RequestMapping(value = "/logout.action")

​    public ModelAndView logout(HttpServletRequest request, HttpServletResponse response) {

​        HttpSession session = request.getSession();

​        session.removeAttribute("sesssion_user_key");      //注销时，删除session中的用户信息。

​        ModelAndView mav = new ModelAndView("redirect:/login/index.action");

​        return mav;

​    }

​    

那么问题来了：     UserLoginBean ulBean = (UserLoginBean) request.getSession().getAttribute("sesssion_user_key");   通过这个来判断是否超时，什么时候超时了，将其设置为null

https://www.cnblogs.com/diewufeixian/p/4221747.html    

1.在web容器中设置（以tomcat为例）

在tomcat-7.0\conf\web.xml中设置，以下是tomcat7.0中默认配置：    

<session-config>

<session-timeout>30</session-timeout>

</session-config>    

​    

​    

2.在工程的web.xml中设置    

<session-config>

<session-timeout>15</session-timeout>

</session-config>    

​    

3.通过java代码设置

session.setMaxInactiveInterval(30*60);//以秒为单位，即在没有活动30分钟后，session将失效    

​    

三种方式优先等级：1 < 2 < 3    

​    

在一般系统中，也可能需要在session失效后做一些操作：

1.控制用户数，当session失效后，系统的用户数减少一个，控制用户数量在一定范围内，确保系统的性能

2.控制一个用户多次登录，当session有效时，如果相同用户登录，就提示已经登录了，当session失效后，就可以不同提示，直接登录

那么如何在session失效后，进行一系列的操作呢？

这里就需要用到监听器了，即当session因为各种原因失效后，监听器就可以监听到，然后执行监听器中定义好的程序就可以了

监听器类为：HttpSessionListener类，有sessionCreated和sessionDestroyed两个方法

自己可以继承这个类，然后分别实现

sessionCreated指在session创建时执行的方法

sessionDestroyed指在session失效时执行的方法

例子：    

public class OnlineUserListener implements HttpSessionListener{

​    public void sessionCreated(HttpSessionEvent event){

​        HttpSession session=event.getSession;

​        String id=session.getId()+session.getCreationTime();

​        SummerConstant.UserMap.put(id,Boolean.TRUE);//添加用户

​    }

​    

​    public void sessionDestroyed(HttpSessionEvent event){

​        HttpSession session=event.getSession;

​        String id=session.getId()+session.getCreationTime();

​        synchronized(this){

​            SummerConstant.USERNum--;//用户数减-

​            SummerConstant.UserMap.remove(id);//从用户组中移除掉，用户组为一个map

​        }

​    }

}    

​    

然后只需要把这个监听器在web.xml中声明就可以了

<listener>

<listener-class>com.demo.OnlineUserListener</listener-class>

</listener>    

​    

​    

====》再次引出问题，session是如何区分用户的，也就是说，每一台电脑的一个用户一个session，互不干扰    

会话（Session）跟踪是Web程序中常用的技术，用来跟踪用户的整个会话。常用的会话跟踪技术是Cookie与Session。

Cookie通过在客户端记录信息确定用户身份，Session通过在服务器端记录信息确定用户身份。    

 

客户端浏览器访问服务器的时候，服务器把客户端信息以某种形式记录在服务器上。这就是Session。客户端浏览器再次访问时只需要从该Session中查找该客户的状态就可以了。

如果说Cookie机制是通过检查客户身上的“通行证”来确定客户身份的话，那么Session机制就是通过检查服务器上的“客户明细表”来确认客户身份。Session相当于程序在服务器上建立的一份客户档案，客户来访的时候只需要查询客户档案表就可以了。

登录界面验证用户登录信息，如果登录正确，就把用户信息以及登录时间保存进Session，然后转到欢迎页面welcome.jsp。welcome.jsp中从Session中获取信息，并将用户资料显示出来。

 

！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！

当多个客户端执行程序时，服务器会保存多个客户端的Session。获取Session的时候也不需要声明获取谁的Session。Session机制决定了当前客户只会获取到自己的Session，而不会获取到别人的Session。各客户的Session也彼此独立，互不可见。

 

Session的生命周期：

Session保存在服务器端。为了获得更高的存取速度，服务器一般把Session放在内存里。每个用户都会有一个独立的Session。如果Session内容过于复杂，当大量客户访问服务器时可能会导致内存溢出。因此，Session里的信息应该尽量精简。

Session在用户第一次访问服务器的时候自动创建。

需要注意只有访问JSP、Servlet等程序时才会创建Session，只访问HTML、IMAGE等静态资源并不会创建Session。如果尚未生成Session，也可以使用request.getSession(true)强制生成Session。

Session生成后，只要用户继续访问，服务器就会更新Session的最后访问时间，并维护该Session。用户每访问服务器一次，无论是否读写Session，服务器都认为该用户的Session“活跃（active）”了一次。

 

 

Session的有效期

由于会有越来越多的用户访问服务器，因此Session也会越来越多。为防止内存溢出，服务器会把长时间内没有活跃的Session从内存删除。这个时间就是Session的超时时间。如果超过了超时时间没访问过服务器，Session就自动失效了。

Session的超时时间为maxInactiveInterval属性，可以通过对应的getMaxInactiveInterval()获取，通过setMaxInactiveInterval(longinterval)修改。

Session的超时时间也可以在web.xml中修改。另外，通过调用Session的invalidate()方法可以使Session失效。

 

Session对浏览器的要求：

虽然Session保存在服务器，对客户端是透明的，它的正常运行仍然需要客户端浏览器的支持。

这是因为Session需要使用Cookie作为识别标志。HTTP协议是无状态的，Session不能依据HTTP连接来判断是否为同一客户，因此服务器向客户端浏览器发送一个名为JSESSIONID的Cookie，它的值为该Session的id（也就是HttpSession.getId()的返回值）。

Session依据该Cookie来识别是否为同一用户。

该Cookie为服务器自动生成的，它的maxAge属性一般为–1，表示仅当前浏览器内有效，并且各浏览器窗口间不共享，关闭浏览器就会失效。

因此同一机器的两个浏览器窗口访问服务器时，会生成两个不同的Session。但是由浏览器窗口内的链接、脚本等打开的新窗口（也就是说不是双击桌面浏览器图标等打开的窗口）除外。这类子窗口会共享父窗口的Cookie，因此会共享一个Session。

 

注意：新开的浏览器窗口会生成新的Session，但子窗口除外。子窗口会共用父窗口的Session。例如，在链接上右击，在弹出的快捷菜单中选择“在新窗口中打开”时，子窗口便可以访问父窗口的Session。

如果客户端浏览器将Cookie功能禁用，或者不支持Cookie怎么办？例如，绝大多数的手机浏览器都不支持Cookie。Java Web提供了另一种解决方案：URL地址重写。

 

URL地址重写是对客户端不支持Cookie的解决方案。URL地址重写的原理是将该用户Session的id信息重写到URL地址中。服务器能够解析重写后的URL获取Session的id。这样即使客户端不支持Cookie，也可以使用Session来记录用户状态。HttpServletResponse类提供了encodeURL(Stringurl)实现URL地址重写，例如：

<td>

    <a
href="<%=response.encodeURL("index.jsp?c=1&wd=Java")
%>">

​    Homepage</a>

</td>

 

该方法会自动判断客户端是否支持Cookie。如果客户端支持Cookie，会将URL原封不动地输出来。如果客户端不支持Cookie，则会将用户Session的id重写到URL中。重写后的输出可能是这样的：

 

<td>

​    <ahref="index.jsp;jsessionid=0CCD096E7F8D97B0BE608AFDC3E1931E?c=

​    1&wd=Java">Homepage</a>

</td>

即在文件名的后面，在URL参数的前面添加了字符串“;jsessionid=XXX”。其中XXX为Session的id。分析一下可以知道，增添的jsessionid字符串既不会影响请求的文件名，也不会影响提交的地址栏参数。用户单击这个链接的时候会把Session的id通过URL提交到服务器上，服务器通过解析URL地址获得Session的id。

​    

如果是页面重定向（Redirection），URL地址重写可以这样写：

<%

​    if(“administrator”.equals(userName))

​    {

​       response.sendRedirect(response.encodeRedirectURL(“administrator.jsp”));

​        return;

​    }

%>

 

效果跟response.encodeURL(String url)是一样的：如果客户端支持Cookie，生成原URL地址，如果不支持Cookie，传回重写后的带有jsessionid字符串的地址。

对于WAP程序，由于大部分的手机浏览器都不支持Cookie，WAP程序都会采用URL地址重写来跟踪用户会话。比如用友集团的移动商街等。    

​    

注意：TOMCAT判断客户端浏览器是否支持Cookie的依据是请求中是否含有Cookie。尽管客户端可能会支持Cookie，但是由于第一次请求时不会携带任何Cookie（因为并无任何Cookie可以携带），URL地址重写后的地址中仍然会带有jsessionid。当第二次访问时服务器已经在浏览器中写入Cookie了，因此URL地址重写后的地址中就不会带有jsessionid了。    

​    

​    

Session中禁止使用Cookie

既然WAP上大部分的客户浏览器都不支持Cookie，索性禁止Session使用Cookie，统一使用URL地址重写会更好一些。Java Web规范支持通过配置的方式禁用Cookie。下面举例说一下怎样通过配置禁止使用Cookie。

打开项目sessionWeb的WebRoot目录下的META-INF文件夹（跟WEB-INF文件夹同级，如果没有则创建），打开context.xml（如果没有则创建），编辑内容如下：

代码1.11 /META-INF/context.xml

<?xml version='1.0' encoding='UTF-8'?>

 

<Context path="/sessionWeb"cookies="false">

 

</Context>

 

或者修改Tomcat全局的conf/context.xml，修改内容如下：

代码1.12  context.xml

<!-- The contents of this file will be loaded for eachweb application -->

<Context cookies="false">

​    <!-- ... 中间代码略 -->

</Context>

部署后TOMCAT便不会自动生成名JSESSIONID的Cookie，Session也不会以Cookie为识别标志，而仅仅以重写后的URL地址为识别标志了。

注意：该配置只是禁止Session使用Cookie作为识别标志，并不能阻止其他的Cookie读写。也就是说服务器不会自动维护名为JSESSIONID的Cookie了，但是程序中仍然可以读写其他的Cookie。    

​    

​    

​    

SESSION拓展：    

在说session是啥之前，我们先来说说为什么会出现session会话，它出现的机理是什么？我们知道，我们用浏览器打开一个网页，用到的是HTTP协议，学过计算机的应该都知道这个协议，它是无状态的，什么是无状态呢？就是说这一次请求和上一次请求是没有任何关系的，互不认识的，没有关联的。但是这种无状态的的好处是快速。    

所以就会带来一个问题就是，我希望几个请求的页面要有关联，比如：我在[www.a.com/login.php](http://www.a.com/login.php)里面登陆了，我在[www.a.com/index.php](http://www.a.com/index.php) 也希望是登陆状态，但是，这是2个不同的页面，也就是2个不同的HTTP请求，这2个HTTP请求是无状态的，也就是无关联的，所以无法单纯的在index.php中读取到它在login.php中已经登陆了！    

那咋搞呢？我不可能这2个页面我都去登陆一遍吧。或者用笨方法这2个页面都去查询数据库，如果有登陆状态，就判断是登陆的了。这种查询数据库的方案虽然可行，但是每次都要去查询数据库不是个事，会造成数据库的压力。    

所以正是这种诉求，这个时候，一个新的客户端存储数据方式出现了：cookie。cookie是把少量的信息存储在用户自己的电脑上，它在一个域名下是一个全局的，只要设置它的存储路径在域名[www.a.com](http://www.a.com/)下 ，那么当用户用浏览器访问时，php就可以从这个域名的任意页面读取cookie中的信息。所以就很好的解决了我在[www.a.com/login.php](http://www.a.com/login.php)页面登陆了，我也可以在[www.a.com/index.php](http://www.a.com/index.php)获取到这个登陆信息了。同时又不用反复去查询数据库。    

虽然这种方案很不错，也很快速方便，但是由于cookie 是存在用户端，而且它本身存储的尺寸大小也有限，最关键是用户可以是可见的，并可以随意的修改，很不安全。那如何又要安全，又可以方便的全局读取信息呢？于是，这个时候，一种新的存储会话机制：session 诞生了。    

好，session 诞生了，从上面的描述来讲，它就是在一次会话中解决2次HTTP的请求的关联，让它们产生联系，让2两个页面都能读取到找个这个全局的session信息。session信息存在于服务器端，所以也就很好的解决了安全问题。    

既然，它也是一种服务区存储数据的方式，肯定也是存在服务器的某个地方了。确实，它存在服务器的/tmp 目录下    

​    

我们主要用PHP中session的机制，其实各种语言都差不多。

如果这个时候，我们需要用到session，那我们第一步怎么办呢？第一步是开启session：

session_start();

这是个无任何返回值的函数，既不会报错，也不会成功。它的作用是开启session，并随机生成一个唯一的32位的session_id，类似于这样：

4c83638b3b0dbf65583181c2f89168ec

session的全部机制也是基于这个session_id    ，它用来区分哪几次请求是一个人发出的。为什么要这样呢？因为HTTP是无状态无关联的，一个页面可能会被成百上千人访问，而且每个人的用户名是不一样的，那么服务器如何区分这次是小王访问的，那次是小名访问的呢？所以就有了找个唯一的session_id 来绑定一个用户。一个用户在一次会话上就是一个session_id，这样成千上万的人访问，服务器也能区分到底是谁在访问了。

​    

session_id 都是一样的：bjvlo4p38cfqkr1hr7pe924ts3，实际情况下，只要不关闭网页，怎么刷新都是一样：    

​    

解惑的时候到了：

每次我们访问一个页面，如果有开启session，也就是有session_start() 时，就会自动生成一个session_id 来标注是这次会话的唯一ID，同时也会自动往cookie里写入一个名字为PHPSESSID的变量，它的值正是session_id，当这次会话没结束，再次访问的时候，服务器会去读取这个PHPSESSID的cookie是否有值有没过期，如果能够读取到，则继续用这个session_id，如果没有，就会新生成一个session_id，同时生成PHPSESSID这个cookie。由于默认生成的这个PHPSESSID cookie是会话，也就是说关闭浏览器就会过期掉，所以，下次重新浏览时，会重新生成一个session_id。    

​    

好，这个是session_id，就用来标识绑定一个用户的，既然session_id生成了。那么当我们往session里面写入数据，是如何保存的，答案是保存在服务器的临时目录里，根据php.ini的配置，我机子上的这个session是存在D:\wamp\tmp 目录里的。    

同样也是用到session_id。session_id是32位的，服务器会用 sess_ + session_id 的形式存在这个临时目录下，    

所以，每一次生成的session_id都会生成一个这样的文件，用来保存这次会话的session信息。    

​    

这个sess文件不会随着客户端的PHPSESSID过期，也一起过期掉，它会一直存在，直到GC扫描到它过期或者使用session_destroy()函数摧毁    

 

我们大致总结下：

HTTP请求一个页面后，如果用到开启session，会去读cookie中的PHPSESSID是否有，如果没有，则会新生成一个session_id，先存入cookie中的PHPSESSID中，再生成一个sess_前缀文件。当有写入$_SESSION的时候，就会往sess_文件里序列化写入数据。当读取的session变量的时候，先会读取cookie中的PHPSESSID，获得session_id，然后再去找这个sess_sessionid文件，来获取对应的数据。由于默认的PHPSESSID是临时的会话，在浏览器关闭后，会消失，所以，我们重新访问的时候，会新生成session_id和sess_这个文件。    

​    

​    

用redis存储session：

上面七七八八说了很多关于session的存储啊机制啊等。现在说说如果用redis 存储session。之前说的都是用文件files存储，现在想用redis，好处有哪些？

 

1.更快的读取和写入速度。redis是直接操纵内存数据的，肯定是要比文件的形式快很多。

 

2.更好的设置好过期时间。文件存储的sess_sdewfrsf文件其实被删除掉还是要考运气的和概率的，很有可能造成sess_文件没即时删除，造成存储磁盘空间过多，和读取SESSION就变慢了。

 

3.更好的分布式同步。设置redis 的主从同步，可以快速的同步session到各台web服务器，比文件存储更加快速。

 

总的说来，用redis来存储SESSION速度更快，性能更高。    

​    

​    

====================================================================Copy-On-Write容器===================================================

Copy-On-Write简称COW，是一种用于程序设计中的优化策略。其基本思路是，从一开始大家都在共享同一个内容，当某个人想要修改这个内容的时候，才会真正把内容Copy出去形成一个新的内容然后再改，这是一种延时懒惰策略。从JDK1.5开始Java并发包里提供了两个使用CopyOnWrite机制实现的并发容器,它们是CopyOnWriteArrayList和CopyOnWriteArraySet

 

CopyOnWrite容器即写时复制的容器。通俗的理解是当我们往一个容器添加元素的时候，不直接往当前容器添加，而是先将当前容器进行Copy，复制出一个新的容器，然后新的容器里添加元素，添加完元素之后，再将原容器的引用指向新的容器。

这样做的好处是我们可以对CopyOnWrite容器进行并发的读，而不需要加锁，因为当前容器不会添加任何元素。所以CopyOnWrite容器也是一种读写分离的思想，读和写不同的容器。

 

CopyOnWriteArrayList的实现原理:

向ArrayList里添加元素，可以发现在添加的时候是需要加锁的，否则多线程写的时候会Copy出N个副本出来。

public boolean add(T e) {

​    final ReentrantLock lock = this.lock;

​    lock.lock();

​    try {

​        Object[] elements = getArray();

​        int len = elements.length;

​        // 复制出新数组

​        Object[] newElements = Arrays.copyOf(elements, len + 1);

​        // 把新元素添加到新数组里

​        newElements[len] = e;

​        // 把原数组引用指向新数组

​        setArray(newElements);

​        return true;

​    } finally {

​        lock.unlock();

​    }

}

读的时候不需要加锁，如果读的时候有多个线程正在向ArrayList添加数据，读还是会读到旧的数据，因为写的时候不会锁住旧的ArrayList。

 

 

CopyOnWrite的应用场景:

CopyOnWrite并发容器用于读多写少的并发场景。比如白名单，黑名单，商品类目的访问和更新场景，假如我们有一个搜索网站，用户在这个网站的搜索框中，输入关键字搜索内容，但是某些关键字不允许被搜索。这些不能被搜索的关键字会被放在一个黑名单当中，黑名单每天晚上更新一次。当用户搜索时，会检查当前关键字在不在黑名单当中，如果在，则提示不能搜索。

 

 

JDK中并没有提供CopyOnWriteMap，我们可以参考CopyOnWriteArrayList来实现一个，基本代码如下：

 

public class CopyOnWriteMap<K, V> implements Map<K, V>, Cloneable {

​    private volatile Map<K, V> internalMap;

​    public CopyOnWriteMap() {

​        internalMap = new HashMap<K, V>();

​    }

​    public V put(K key, V value) {

​        synchronized (this) {

​            Map<K, V> newMap = new HashMap<K, V>(internalMap);

​            V val = newMap.put(key, value);

​            internalMap = newMap;

​            return val;

​        }

​    }

​    public V get(Object key) {

​        return internalMap.get(key);

​    }

​    public void putAll(Map<? extends K, ? extends V> newData) {

​        synchronized (this) {

​            Map<K, V> newMap = new HashMap<K, V>(internalMap);

​            newMap.putAll(newData);

​            internalMap = newMap;

​        }

​    }

}

 

 

CopyOnWrite并发容器用于读多写少的并发场景。比如白名单，黑名单，商品类目的访问和更新场景，假如我们有一个搜索网站，用户在这个网站的搜索框中，输入关键字搜索内容，但是某些关键字不允许被搜索。这些不能被搜索的关键字会被放在一个黑名单当中，黑名单每天晚上更新一次。当用户搜索时，会检查当前关键字在不在黑名单当中，如果在，则提示不能搜索。

 

使用批量添加。因为每次添加，容器每次都会进行复制，所以减少添加次数，可以减少容器的复制次数。如使用上面代码里的putAll方法。

 

CopyOnWrite容器有很多优点，但是同时也存在两个问题，即内存占用问题和数据一致性问题。

 

1.内存占用问题。因为CopyOnWrite的写时复制机制，所以在进行写操作的时候，内存里会同时驻扎两个对象的内存，旧的对象和新写入的对象（注意:在复制的时候只是复制容器里的引用，只是在写的时候会创建新对象添加到新容器里，而旧容器的对象还在使用，所以有两份对象内存）。如果这些对象占用的内存比较大，比如说200M左右，那么再写入100M数据进去，内存就会占用300M，那么这个时候很有可能造成频繁的Yong GC和Full GC。之前我们系统中使用了一个服务由于每晚使用CopyOnWrite机制更新大对象，造成了每晚15秒的Full GC，应用响应时间也随之变长。

 

针对内存占用问题，可以通过压缩容器中的元素的方法来减少大对象的内存消耗，比如，如果元素全是10进制的数字，可以考虑把它压缩成36进制或64进制。或者不使用CopyOnWrite容器，而使用其他的并发容器，如ConcurrentHashMap。

 

2.数据一致性问题

CopyOnWrite容器只能保证数据的最终一致性，不能保证数据的实时一致性。所以如果你希望写入的的数据，马上能读到，请不要使用CopyOnWrite容器。

 

====================================================================HashMap的put方法返回值====================================================================

例子：

 

public class Test {

​    public static void main(String[] args) {

​        Map<String, String> map = new HashMap<String, String>();

​        String p1 = map.put("11", "22");

​        System.out.println("p1:" + p1);

​        String p2 = map.put("33", "44");

​        System.out.println("p2:" + p2);

​        String value1 = map.get("11");

​        System.out.println("value1:" + value1);

​        String p3 = map.put("11", "44");

​        System.out.println("p3：" + p3);

​        String value2 = map.get("11");

​        System.out.println("value2:" + value2);

​    }

}

 

输出结果：

 

p1:null

p2:null

value1:22

p3：22

value2:44

 

说明：put方法返回值为null或者value；

 

如果key没有重复，put成功，则返回null，如p1、p2；

 

如果key重复了，返回的是map.get(key)，也就是当前这个key对应的value，如上面的p3，key="11"，而p1的key也是"11"，p1与p3重复，返回的是p1的value="22"，并且将p3覆盖掉p1

 

也即：  put 要么返回 null， 要么返回旧值。   当put操作覆盖时，返回旧的value值。

 

 

====================================================================并发编程的总结和思考====================================================================

Java Web中的Servlet程序在Servlet容器的支持下采用单实例多线程的工作模式，Servlet容器为你处理了并发问题。

 

 

 

 

====================================================================哲学家进餐====================================================================

五个哲学家围坐在一张圆桌周围，每个哲学家面前都有一盘通心粉。由于通心粉很滑，所以需要两把叉子才能夹住。相邻两个盘子之间放有一把叉子如下图所示。哲学家的生活中有两种交替活动时段：即吃饭和思考。当一个哲学家觉得饿了时，他就试图分两次去取其左边和右边的叉子，每次拿一把，但不分次序。如果成功地得到了两把叉子，就开始吃饭，吃完后放下叉子继续思考。

 

 

注意点：1.不能每个哲学家都先拿左边的筷子，应该交错拿，1号先拿左边，2号先拿右边，3号先拿左边，4号先拿右边

​        2.最多只能有4个哲学家同时进餐

​        3.代码实现 Semaphore

 

class AppContext {

​    public static final int NUM_OF_FORKS = 5;   // 叉子数量(资源)

​    public static final int NUM_OF_PHILO = 5;   // 哲学家数量(线程)

​    public static Semaphore[] forks;    // 叉子的信号量

​    public static Semaphore counter;    // 哲学家的信号量

​    static {

​        forks = new Semaphore[NUM_OF_FORKS];

​        for (int i = 0, len = forks.length; i < len; ++i) {

​            forks[i] = new Semaphore(1);    // 每个叉子的信号量为1

​        }

​        counter = new Semaphore(NUM_OF_PHILO - 1);  // 如果有N个哲学家，最多只允许N-1人同时取叉子

​    }

​    /**

​     \* 取得叉子

​     \* @param index 第几个哲学家

​     \* @param leftFirst 是否先取得左边的叉子

​     \* @throws InterruptedException

​     */

​    public static void putOnFork(int index, boolean leftFirst) throws InterruptedException {

​        if(leftFirst) {

​            forks[index].acquire();

​            forks[(index + 1) % NUM_OF_PHILO].acquire();

​        }

​        else {

​            forks[(index + 1) % NUM_OF_PHILO].acquire();

​            forks[index].acquire();

​        }

​    }

​    /**

​     \* 放回叉子

​     \* @param index 第几个哲学家

​     \* @param leftFirst 是否先放回左边的叉子

​     \* @throws InterruptedException

​     */

​    public static void putDownFork(int index, boolean leftFirst) throws InterruptedException {

​        if(leftFirst) {

​            forks[index].release();

​            forks[(index + 1) % NUM_OF_PHILO].release();

​        }

​        else {

​            forks[(index + 1) % NUM_OF_PHILO].release();

​            forks[index].release();

​        }

​    }

}

/**

\* 哲学家

\* @author 骆昊

*

*/

class Philosopher implements Runnable {

​    private int index;      // 编号

​    private String name;    // 名字

​    public Philosopher(int index, String name) {

​        this.index = index;

​        this.name = name;

​    }

​    @Override

​    public void run() {

​        while(true) {

​            try {

​                AppContext.counter.acquire();

​                boolean leftFirst = index % 2 == 0;

​                AppContext.putOnFork(index, leftFirst);

​                System.out.println(name + "正在吃意大利面（通心粉）...");   // 取到两个叉子就可以进食

​                AppContext.putDownFork(index, leftFirst);

​                AppContext.counter.release();

​            } catch (InterruptedException e) {

​                e.printStackTrace();

​            }

​        }

​    }

}

public class Test04 {

​    public static void main(String[] args) {

​        String[] names = { "骆昊", "王大锤", "张三丰", "杨过", "李莫愁" };   // 5位哲学家的名字

//      ExecutorService es = Executors.newFixedThreadPool(AppContext.NUM_OF_PHILO); // 创建固定大小的线程池

//      for(int i = 0, len = names.length; i < len; ++i) {

//          es.execute(new Philosopher(i, names[i]));   // 启动线程

//      }

//      es.shutdown();

​        for(int i = 0, len = names.length; i < len; ++i) {

​            new Thread(new Philosopher(i, names[i])).start();

​        }

​    }

}

 

 

====================================================================回调机制====================================================================

 

就是A类中调用B类中的某个方法C，然后B类中反过来调用A类中的方法D，D这个方法就叫回调方法

 

线程A有操作 a,b ，其中a是调用线程B的方法c，线程B的方法c可能很耗时，A必须完成a才能执行b，c的执行过程中A一直阻塞在那儿。

====》   回调：

A调用线程B的方法c后继续做自己的事 d、e、f ，这时候线程B的方法c完成后主动去掉A的b，即可。

 

 

有一天小王遇到一个很难的问题，问题是“1 + 1 = ?”，就打电话问小李，小李一下子也不知道，就跟小王说，等我办完手上的事情，就去想想答案，小王也不会傻傻的拿着电话去等小李的答案吧，于是小王就对小李说，我还要去逛街，你知道了答案就打我电话告诉我，于是挂了电话，自己办自己的事情，过了一个小时，小李打了小王的电话，告诉他答案是2

 

 

 

/**

\* 这是一个回调接口

\* @author xiaanming

*

*/

public interface CallBack {  

​    /**

​     \* 这个是小李知道答案时要调用的函数告诉小王，也就是回调函数

​     \* @param result 是答案

​     */

​    public void solve(String result);  

}

 

\* 这个是小王

\* @author xiaanming

\* 实现了一个回调接口CallBack，相当于----->背景一

*/

public class Wang implements CallBack {  

​    /**

​     \* 小李对象的引用

​     \* 相当于----->背景二

​     */

​    private Li li;   

​    /**

​     \* 小王的构造方法，持有小李的引用

​     \* @param li

​     */

​    public Wang(Li li){  

​        this.li = li;  

​    }  

​    /**

​     \* 小王通过这个方法去问小李的问题

​     \* @param question  就是小王要问的问题,1 + 1 = ?

​     */

​    public void askQuestion(final String question){  

​        //这里用一个线程就是异步，  

​        new Thread(new Runnable() {  

​            @Override

​            public void run() {  

​                /**

​                 \* 小王调用小李中的方法，在这里注册回调接口

​                 \* 这就相当于A类调用B的方法C

​                 */

​                li.executeMessage(Wang.this, question);   

​            }  

​        }).start();  

​        //小网问完问题挂掉电话就去干其他的事情了，诳街去了  

​        play();  

​    }  

​    public void play(){  

​        System.out.println("我要逛街去了");  

​    }  

​    /**

​     \* 小李知道答案后调用此方法告诉小王，就是所谓的小王的回调方法

​     */

​    @Override

​    public void solve(String result) {  

​        System.out.println("小李告诉小王的答案是--->" + result);  

​    }  

}

 

/**

\* 这个就是小李啦

\* @author xiaanming

*

*/

public class Li {  

​    /**

​     \* 相当于B类有参数为CallBack callBack的f()---->背景三

​     \* @param callBack   

​     \* @param question  小王问的问题

​     */

​    public void executeMessage(CallBack callBack, String question){  

​        System.out.println("小王问的问题--->" + question);  

​        //模拟小李办自己的事情需要很长时间  

​        for(int i=0; i<10000;i++){  

​        }  

​        /**

​         \* 小李办完自己的事情之后想到了答案是2

​         */

​        String result = "答案是2";  

​        /**

​         \* 于是就打电话告诉小王，调用小王中的方法

​         \* 这就相当于B类反过来调用A的方法D

​         */

​        callBack.solve(result);   

​    }  

}

 

 

====================================================================HBase====================================================================

Apache HBase 的官方网站为：http://hbase.apache.org/。

利用 HBase 技术可在廉价 PC 上搭建起大规模结构化存储集群。

 

HBase 是 Google Bigtable 的开源实现，类似 Google Bigtable 利用 GFS 作为其文件存储系统，HBase 利用 Hadoop HDFS 作为其文件存储系统；Google 运行 MapReduce 来处理 Bigtable 中的海量数据，HBase 同样利用 Hadoop MapReduce 来处理 HBase 中的海量数据；Google Bigtable 利用 Chubby 作为协同服务，HBase 利用 Zookeeper 作为对应。

 

HBase 的应用场景：

首先，确信有足够多数据，如果有上亿或上千亿行数据，HBase 是很好的备选。如果只有上千或上百万行，则用传统的R DBMS 可能是更好的选择。因为所有数据可以在一两个节点保存，集群其他节点可能闲置。

 

Hbase 的优点：

列的可以动态增加，并且列为空就不存储数据，节省存储空间

Hbase 自动切分数据，使得数据存储自动具有水平扩展

Hbase 可以提供高并发读写操作的支持

与 Hadoop MapReduce 相结合有利于数据分析

容错性

版权免费

非常灵活的模式设计（或者说没有固定模式的限制）

可以跟 Hive 集成，使用类 SQL 查询

自动故障转移

客户端接口易于使用

行级别原子性，即，PUT 操作一定是完全成功或者完全失败

 

Hbase 的缺点：

不能支持条件查询，只支持按照 row key 来查询

容易产生单点故障（在只使用一个 HMaster 的时候）

不支持事务

JOIN 不是数据库层支持的，而需要用 MapReduce

只能在逐渐上索引和排序

没有内置的身份和权限认证

 

 

====================================================================线程优先级====================================================================

Java中通过getPriority和setPriority方法获取和设置线程的优先级。

Thread类提供了三个表示优先级的常量：MIN_PRIORITY优先级最低，为1；NORM_PRIORITY是正常的优先级；为5，MAX_PRIORITY优先级最高，为10。我们创建线程对象后，如果不显示的设置优先级的话，默认为5。

 

【Demo】:线程优先级

/**

\* 优先级

*/

class PriorityThread implements Runnable{

   @Override

   public void run() {

​      for (int i = 0; i < 1000; i ++) {

​         System.out.println(Thread.currentThread().getName() + ": " + i);

​      }

   }

}

调用代码：

 

//创建三个线程

Thread thread1 = new Thread(new PriorityThread(), "Thread1");

Thread thread2 = new Thread(new PriorityThread(), "Thread2");

Thread thread3 = new Thread(new PriorityThread(), "Thread3");

//设置优先级

thread1.setPriority(Thread.MAX_PRIORITY);

thread2.setPriority(8);

//开始执行线程

thread3.start();

thread2.start();

thread1.start();

从结果中我们可以看到线程thread1明显比线程thread3执行的快。

 

让一个高优先级的线程和低优先级的线程同时争夺一个锁，看看哪个最先完成。

当然并不一定是高优先级一定先完成。再多次运行后发现，高优先级完成的概率比较大，但是低优先级还是有可能先完成的。

 

 

 

 

 

 

 

====================================================================URL====================================================================

1.URLEncoder

 

假设你有个HTTP的服务端点http://foo.com/search，它接受一个查询参数p，p的值就是要查找的字符串。如果你搜索”You & I”这个串的话，你第一次创建的搜索的URL可能是这样：http://foo.com/search?q=You & I。这个当然没法工作，因为&是分隔查询参数name/value对的分隔符。如果你拿到这个错乱的URL串的话，你对它简直束手无策，因为首先你就没法正确的解析它。

那好，我们来使用下URLEncoder。URLEncoder.encode(“You & I”, “UTF-8″)是结果是You+%26+I。这个%26解码之后就是&，而+号在查询串中代表的就是空格，因此这个URL是能正常工作的。

现在假设你想使用你的查询串来拼接URL路径，而不是放到URL参数里面。很明显，http://foo.com/search/You & I是错误的。不幸的是，URLEncoder.encode()的结果也是错的。http://foo.com/search/You+%26+I解码后会得到/search/You+&+I，因为+号在URL路径中是不会解析成空格的。

 

 

====================================================================Java transient====================================================================

我们都知道一个对象只要实现了Serilizable接口，这个对象就可以被序列化，java的这种序列化模式为开发者提供了很多便利，我们可以不必关系具体序列化的过程，只要这个类实现了Serilizable接口，这个类的所有属性和方法都会自动序列化。

 

然而在实际开发过程中，我们常常会遇到这样的问题，这个类的有些属性需要序列化，而其他属性不需要被序列化，打个比方，如果一个用户有一些敏感信息（如密码，银行卡号等），为了安全起见，不希望在网络操作（主要涉及到序列化操作，本地序列化缓存也适用）中被传输，这些信息对应的变量就可以加上transient关键字。换句话说，这个字段的生命周期仅存于调用者的内存中而不会写到磁盘里持久化。

 

总之，java 的transient关键字为我们提供了便利，你只需要实现Serilizable接口，将不需要序列化的属性前添加关键字transient，序列化对象的时候，这个属性就不会序列化到指定的目的地中。

 

public class TransientTest {

​    public static void main(String[] args) {

​        User user = new User();

​        user.setUsername("Alexia");

​        user.setPasswd("123456");

​        System.out.println("read before Serializable: ");

​        System.out.println("username: " + user.getUsername());

​        System.err.println("password: " + user.getPasswd());

​        try {

​            ObjectOutputStream os = new ObjectOutputStream(

​                    new FileOutputStream("C:/user.txt"));

​            os.writeObject(user); // 将User对象写进文件

​            os.flush();

​            os.close();

​        } catch (FileNotFoundException e) {

​            e.printStackTrace();

​        } catch (IOException e) {

​            e.printStackTrace();

​        }

​        try {

​            ObjectInputStream is = new ObjectInputStream(new FileInputStream(

​                    "C:/user.txt"));

​            user = (User) is.readObject(); // 从流中读取User的数据

​            is.close();

​            System.out.println("\nread after Serializable: ");

​            System.out.println("username: " + user.getUsername());

​            System.err.println("password: " + user.getPasswd());

​        } catch (FileNotFoundException e) {

​            e.printStackTrace();

​        } catch (IOException e) {

​            e.printStackTrace();

​        } catch (ClassNotFoundException e) {

​            e.printStackTrace();

​        }

​    }

}

class User implements Serializable {

​    private static final long serialVersionUID = 8294180014912103005L;  

​    private String username;

​    private transient String passwd;

​    public String getUsername() {

​        return username;

​    }

​    public void setUsername(String username) {

​        this.username = username;

​    }

​    public String getPasswd() {

​        return passwd;

​    }

​    public void setPasswd(String passwd) {

​        this.passwd = passwd;

​    }

}

 

read before Serializable:

username: Alexia

password: 123456

read after Serializable:

username: Alexia

password: null

 

 

transient使用小结

1）一旦变量被transient修饰，变量将不再是对象持久化的一部分，该变量内容在序列化后无法获得访问。

2）transient关键字只能修饰变量，而不能修饰方法和类。注意，本地变量是不能被transient关键字修饰的。变量如果是用户自定义类变量，则该类需要实现Serializable接口。

3）被transient关键字修饰的变量不再能被序列化，一个静态变量不管是否被transient修饰，均不能被序列化。

 

第三点可能有些人很迷惑，因为发现在User类中的username字段前加上static关键字后，程序运行结果依然不变，即static类型的username也读出来为“Alexia”了，这不与第三点说的矛盾吗？实际上是这样的：第三点确实没错（一个静态变量不管是否被transient修饰，均不能被序列化），反序列化后类中static型变量username的值为当前JVM中对应static变量的值，这个值是JVM中的不是反序列化得出的，不相信？好吧，下面我来证明：

public class TransientTest {

​    public static void main(String[] args) {

​        User user = new User();

​        user.setUsername("Alexia");

​        user.setPasswd("123456");

​        System.out.println("read before Serializable: ");

​        System.out.println("username: " + user.getUsername());

​        System.err.println("password: " + user.getPasswd());

​        try {

​            ObjectOutputStream os = new ObjectOutputStream(

​                    new FileOutputStream("C:/user.txt"));

​            os.writeObject(user); // 将User对象写进文件

​            os.flush();

​            os.close();

​        } catch (FileNotFoundException e) {

​            e.printStackTrace();

​        } catch (IOException e) {

​            e.printStackTrace();

​        }

​        try {

​            // 在反序列化之前改变username的值

​            User.username = "jmwang";

​            ObjectInputStream is = new ObjectInputStream(new FileInputStream(

​                    "C:/user.txt"));

​            user = (User) is.readObject(); // 从流中读取User的数据

​            is.close();

​            System.out.println("\nread after Serializable: ");

​            System.out.println("username: " + user.getUsername());

​            System.err.println("password: " + user.getPasswd());

​        } catch (FileNotFoundException e) {

​            e.printStackTrace();

​        } catch (IOException e) {

​            e.printStackTrace();

​        } catch (ClassNotFoundException e) {

​            e.printStackTrace();

​        }

​    }

}

class User implements Serializable {

​    private static final long serialVersionUID = 8294180014912103005L;  

​    public static String username;

​    private transient String passwd;

​    public String getUsername() {

​        return username;

​    }

​    public void setUsername(String username) {

​        this.username = username;

​    }

​    public String getPasswd() {

​        return passwd;

​    }

​    public void setPasswd(String passwd) {

​        this.passwd = passwd;

​    }

}

 

read before Serializable:

username: Alexia

password: 123456

read after Serializable:

username: jmwang

password: null

 

 

 

 

 

====================================================================对象输入输出流 ObjectInputStream 、 ObjectOutputStream （对象序列化与反序列化）====================================================================

对象的输出流将指定的对象写入到文件的过程，就是将对象序列化的过程，对象的输入流将指定序列化好的文件读出来的过程，就是对象反序列化的过程。既然对象的输出流将对象写入到文件中称之为对象的序列化，那么可想而知对象所对应的class必须要实现Serializable接口。

 

\1. 如果对象需要被写出到文件上，那么对象所属的类必须要实现Serializable接口。 Serializable接口没有任何的方法，是一个标识接口而已。

\2. 对象的反序列化创建对象的时候并不会调用到构造方法的、（这点文中没有说到，想要验证的同学在构造方法后面加一句System.out.println("构造方法执行吗？");，实际上构造方法是不执行的，自然这句话也没有输出了）

\3. serialVersionUID 是用于记录class文件的版本信息的，serialVersionUID这个数字是通过一个类的类名、成员、包名、工程名算出的一个数字。

\4. 使用ObjectInputStream反序列化的时候，ObjeectInputStream会先读取文件中的serialVersionUID，然后与本地的class文件的serialVersionUID

进行对比，如果这两个id不一致，反序列则失败。

\5. 如果序列化与反序列化的时候可能会修改类的成员，那么最好一开始就给这个类指定一个serialVersionUID，如果一类已经指定的serialVersionUID，然后

在序列化与反序列化的时候，jvm都不会再自己算这个 class的serialVersionUID了。

\6. 如果一个对象某个数据不想被序列化到硬盘上，可以使用关键字transient修饰。

\7. 如果一个类维护了另外一个类的引用，则另外一个类也需要实现Serializable接口。

 

 

 

 

====================================================================为什么HashMap是线程不安全的====================================================================

要回答这个问题就要先来简单了解一下HashMap源码中的使用的存储结构(这里引用的是Java 8的源码，与7是不一样的)和它的扩容机制。

 

HashMap使用的存储结构:

 

transient Node<K,V>[] table;

static class Node<K,V> implements Map.Entry<K,V> {

​        final int hash;

​        final K key;

​        V value;

​        Node<K,V> next;

}

 

可以看到HashMap内部存储使用了一个Node数组(默认大小是16)，而Node类包含一个类型为Node的next的变量，也就是相当于一个链表，所有hash值相同(即产生了冲突)的key会存储到同一个链表里

需要注意的是，在Java 8中如果hash值相同的key数量大于指定值(默认是8)时使用平衡树来代替链表，这会将get()方法的性能从O(n)提高到O(logn)。

 

Java 8中使用平衡树来替代链表存储冲突的元素。这意味着我们可以将最坏情况下的性能从O(n)提高到O(logn)。

在Java 8中使用常量TREEIFY_THRESHOLD来控制是否切换到平衡树来存储。目前，这个常量值是8，这意味着当有超过8个元素的索引一样时，HashMap会使用树来存储它们。

 

 

http://www.importnew.com/21396.html

 

 

 

====================================================================并发 并行====================================================================

并行：

 

|——————————————————>|

|

|..................>|

 

并发:

|                  |

|-->..>-->..>-->..>|

|                  |

 

 

 

启动一个线程是调用run()还是start()方法？

答：启动一个线程是调用start()方法，使线程所代表的虚拟处理机处于可运行状态，这意味着它可以由JVM 调度并执行，这并不意味着线程就会立即运行。run()方法是线程启动后要进行回调（callback）的方法。

 

Thread类的sleep()方法和对象的wait()方法都可以让线程暂停执行，它们有什么区别?

答：sleep()方法（休眠）是线程类（Thread）的静态方法，调用此方法会让当前线程暂停执行指定的时间，将执行机会（CPU）让给其他线程，但是对象的锁依然保持，因此休眠时间结束后会自动恢复（线程回到就绪状态，请参考第66题中的线程状态转换图）。wait()是Object类的方法，调用对象的wait()方法导致当前线程放弃对象的锁（线程暂停执行），进入对象的等待池（wait pool），只有调用对象的notify()方法（或notifyAll()方法）时才能唤醒等待池中的线程进入等锁池（lock pool），如果线程重新获得对象的锁就可以进入就绪状态。

 

线程的sleep()方法和yield()方法有什么区别？

答：

① sleep()方法给其他线程运行机会时不考虑线程的优先级，因此会给低优先级的线程以运行的机会；yield()方法只会给相同优先级或更高优先级的线程以运行的机会；

② 线程执行sleep()方法后转入阻塞（blocked）状态，而执行yield()方法后转入就绪（ready）状态；

③ sleep()方法声明抛出InterruptedException，而yield()方法没有声明任何异常；

④ sleep()方法比yield()方法（跟操作系统CPU调度相关）具有更好的可移植性。

 

====================================================================线程中断====================================================================

public void Thread.interrupt() // 中断线程

public boolean Thread.isInterrupted() // 判断是否被中断

public static boolean Thread.interrupted() // 判断是否被中断，并清除当前中断状态

 

如果不了解Java的中断机制，这样的一种解释极容易造成误解，认为调用了线程的interrupt方法就一定会中断线程。

其实，Java的中断是一种协作机制。也就是说调用线程对象的interrupt方法并不一定就中断了正在运行的线程，它只是要求线程自己在合适的时机中断自己。

每个线程都有一个boolean的中断状态（不一定就是对象的属性，事实上，该状态也确实不是Thread的字段），interrupt方法仅仅只是将该状态置为true。对于非阻塞中的线程, 只是改变了中断状态, 即Thread.isInterrupted()将返回true，并不会使程序停止;

 

不客气地说，至少有一半人认为，线程的”中断”就是让线程停止。

在java中，线程的中断(interrupt)只是改变了线程的中断状态，至于这个中断状态改变后带来的结果，那是无法确定的，有时它更是让停止中的线程继续执行的唯一手段。不但不是让线程停止运行，反而是继续执行线程的手段。

 

interrupt唤醒wait线程，唤醒Sleep线程

 

例子：

public class ThreadTest extends Thread {

​    private volatile boolean finished = false;

​    

​    public void stopMe()

​    {

​        finished = true;

​        System.out.println("now finished:" + finished);

​        this.interrupt(); //① 产生一个中断

​    }

​    

​    @Override

​    public void run()

​    {

​        int i = 0;

​        while (!finished)

​        {

​             i++;

​             if( i == 1000){

​                 System.out.println("i == 1000 now");

​                 i=1;

​             }

​        }

​    }

}

 

public static void main(String[] args) {

​    ThreadTest threadTest = new ThreadTest();

​    threadTest.start();

​    threadTest.interrupt();

}

 

i == 1000 now     永远不会停止;

 

 

 

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

在一个线程对象上调用interrupt()方法，真正有影响的是wait，join，sleep方法，当然这三个方法包括它们的重载方法。

 

如果一个线程被调用了interrupt()后，它的状态是阻塞状态的。而且这个状态是由于正在执行wait，join，sleep的线程导致的，那么是会改变线程的运行结果.

 

对于wait中的等待notify、notifyAll换新的线程，其实这个线程已经“暂停”执行，因为它正在某一对象的休息室中，这时如果它的中断状态被改变，那么它就会抛出异常。这个InterruptedException异常不是线程抛出的，而是wait方法，也就是对象的wait方法内部会不断检查在此对象上休息的线程的状态，如果发现哪个线程的状态被置为已中断，则会抛出InterruptedException，意思就是这个线程不能再等待了，其意义就等同于唤醒它了，然后执行catch中的代码。

 

这里唯一的区别是，被nortify/All唤醒的线程会继续执行wait下面的语句，而在wait 中被中断的线程则将控制权交给了catch语句。

 

​    

=======================================================================通过Future来实现取消=======================================================================

ExecutorService.submit将返回一个Future来描述任务。Future拥有一个cancel方法，该方法带有一个boolean类型的参数mayInterruptIfRunning，表示取消操作是否成功。

如果mayInterruptIfRunning为true并且任务当前正在某个线程运行，那么这个线程能被中断。如果这个参数为false，那么意味着“若任务还没启动，就不要运行它”，

这种方式应该用于那些不处理中断的任务中。当Future.get抛出InterruptedException或TimeoutException时，如果你知道不再需要结果，那么就可以调用Futuure.cancel来取消任务。

 

有个值得关注的问题就是当任务还在执行的时候用户调用cancel(true)方法能否真正让任务停止执行呢？

在前面的分析中我们直到，当调用cancel(true)方法的时候，实际执行还是Thread.interrupt()方法，而interrupt()方法只是设置中断标志位，如果被中断的线程处于sleep()、wait()或者join()逻辑中则会抛出InterruptedException异常。

因此结论是:cancel(true)并不一定能够停止正在执行的异步任务。

 

public boolean cancel(boolean mayInterruptIfRunning) {

​    // 1. 如果任务已经结束，则直接返回false

​    if (state != NEW)

​        return false;

​    // 2. 如果需要中断任务执行线程

​    if (mayInterruptIfRunning) {

​        // 2.1. 把任务状态从NEW转化到INTERRUPTING

​        if (!UNSAFE.compareAndSwapInt(this, stateOffset, NEW, INTERRUPTING))

​            return false;

​        Thread t = runner;

​        // 2.2. 中断任务执行线程

​        if (t != null)

​            t.interrupt();

​        // 2.3. 修改状态为INTERRUPTED

​        UNSAFE.putOrderedInt(this, stateOffset, INTERRUPTED); // final state

​    }

​    // 3. 如果不需要中断任务执行线程，则直接把状态从NEW转化为CANCELLED

​    else if (!UNSAFE.compareAndSwapInt(this, stateOffset, NEW, CANCELLED))

​        return false;

​    // 4.

​    finishCompletion();

​    return true;

}

 

 

 

 

 

public class ThreadTest extends Thread {

​    private volatile boolean finished = false;

​    

​    public void stopMe()

​    {

​        finished = true;

​        System.out.println("now finished:" + finished);

​        this.interrupt(); //① 产生一个中断

​    }

​    

​    @Override

​    public void run()

​    {

​        int i = 0;

​        while (!finished)

​        {

​             i++;

​             if( i == 1000){

​                 System.out.println("i == 1000 now");

​                 i=1;

​             }

​        }

​    }

}

 

public static void main(String[] args) throws InterruptedException {

​    ThreadTest threadTest = new ThreadTest();

​    //threadTest.start();

​    //threadTest.interrupt();

​    

​    

​    ExecutorService es = Executors.newFixedThreadPool(1);

​    Future f = es.submit(threadTest);

​    Thread.currentThread().sleep(3000);

​    f.cancel(false);

}

 

i == 1000 now     永远不会停止;

 

 

=======================================================================怎么才能终止线程呢？=======================================================================

volatile  标记

 

public class ThreadTest extends Thread {

​    private volatile boolean finished = false;

 

​    public void stopMe() {

​        finished = true;

​        System.out.println("now finished:" + finished);

​        this.interrupt(); // ① 产生一个中断

​    }

 

​    @Override

​    public void run() {

​        int i = 0;

​        while (!finished) {

​            i++;

​            if (i == 1000) {

​                System.out.println("i == 1000 now");

​                i = 1;

​            }

​        }

​    }

 

​    public boolean isFinished() {

​        return finished;

​    }

 

​    public void setFinished(boolean finished) {

​        this.finished = finished;

​    }

}

 

 

public static void main(String[] args) throws InterruptedException {

​    ThreadTest threadTest = new ThreadTest();

​    ExecutorService es = Executors.newFixedThreadPool(1);

​    Future f = es.submit(threadTest);

​    Thread.currentThread().sleep(3000);

​    threadTest.setFinished(true);

}

 

 

法2：

Thread.currentThread().isInterrupted()  ？？？？？

 

 

=======================================================================Java垃圾回收机制=======================================================================

一.如何确定某个对象是“垃圾”？

在java中是通过引用来和对象进行关联的，也就是说如果要操作对象，必须通过引用来进行。那么很显然一个简单的办法就是通过引用计数来判断一个对象是否可以被回收。不失一般性，如果一个对象没有任何引用与之关联，则说明该对象基本不太可能在其他地方被使用到，那么这个对象就成为可被回收的对象了。这种方式成为引用计数法。

 

这种方式的特点是实现简单，而且效率较高，但是它无法解决循环引用的问题，因此在Java中并没有采用这种方式（Python采用的是引用计数法）。看下面这段代码：

 

public class Main {

​    public static void main(String[] args) {

​        MyObject object1 = new MyObject();

​        MyObject object2 = new MyObject();

​        object1.object = object2;

​        object2.object = object1;

​        object1 = null;

​        object2 = null;

​    }

}

class MyObject{

​    public Object object = null;

}

最后面两句将object1和object2赋值为null，也就是说object1和object2指向的对象已经不可能再被访问，但是由于它们互相引用对方，导致它们的引用计数都不为0，那么垃圾收集器就永远不会回收它们。

 

为了解决这个问题，在Java中采取了 可达性分析法。该方法的基本思想是通过一系列的“GC Roots”对象作为起点进行搜索，如果在“GC Roots”和一个对象之间没有可达路径，则称该对象是不可达的，不过要注意的是被判定为不可达的对象不一定就会成为可回收对象。被判定为不可达的对象要成为可回收对象必须至少经历两次标记过程，如果在这两次标记过程中仍然没有逃脱成为可回收对象的可能性，则基本上就真的成为可回收对象了。

 

 

最后总结一下平常遇到的比较常见的将对象判定为可回收对象的情况：

1）显示地将某个引用赋值为null或者将已经指向某个对象的引用指向新的对象，比如下面的代码：

Object obj = new Object();

obj = null;

Object obj1 = new Object();

Object obj2 = new Object();

obj1 = obj2;

 

2）局部引用所指向的对象，比如下面这段代码：

void fun() {

​    for(int i=0;i<10;i++) {

​        Object obj = new Object();

​        System.out.println(obj.getClass());

​    }   

}

循环每执行完一次，生成的Object对象都会成为可回收的对象。

 

3）只有弱引用与其关联的对象，比如：

WeakReference<String> wr = new WeakReference<String>(new String("world"));

 

 

http://www.importnew.com/21218.html

 

 

 

Java的四种引用方式:

  强引用，软引用，弱引用，虚引用

  

１．强引用

是指创建一个对象并把这个对象赋给一个引用变量。

Object object =new Object();  object永远不会被垃圾回收？？

String str ="hello";   str永远不会被垃圾回收？？

强引用有引用变量指向时永远不会被垃圾回收，JVM宁愿抛出OutOfMemory错误也不会回收这种对象。

 

public class Main {  

​    public static void main(String[] args) {  

​        new Main().fun1();  

​    }  

​       

​    public void fun1() {  

​        Object object = new Object();  

​        Object[] objArr = new Object[1000];  

​    }

}    

当运行至Object[] objArr = new Object[1000];这句时，如果内存不足，JVM会抛出OOM错误也不会回收object指向的对象。不过要注意的是，当fun1运行完之后，object和objArr都已经不存在了，所以它们指向的对象都会被JVM回收。

如果想中断强引用和某个对象之间的关联，可以显示地将引用赋值为null，这样一来的话，JVM在合适的时间就会回收该对象。

比如Vector类的clear方法中就是通过将引用赋值为null来实现清理工作的：

 

2.软引用（SoftReference） (软可及对象)

如果一个对象具有软引用，内存空间足够，垃圾回收器就不会回收它；

 

如果内存空间不足了，就会回收这些对象的内存。只要垃圾回收器没有回收它，该对象就可以被程序使用。

 

软引用可用来实现内存敏感的高速缓存,比如网页缓存、图片缓存等。使用软引用能防止内存泄露，增强程序的健壮性。   

SoftReference的特点是它的一个实例保存对一个Java对象的软引用， 该软引用的存在不妨碍垃圾收集线程对该Java对象的回收。

 

也就是说，一旦SoftReference保存了对一个Java对象的软引用后，在垃圾线程对 这个Java对象回收前，SoftReference类所提供的get()方法返回Java对象的强引用。

 

另外，一旦垃圾线程回收该Java对象之 后，get()方法将返回null。

 

MyObject aRef = new  MyObject();  

SoftReference aSoftRef=new SoftReference(aRef);  

此时，对于这个MyObject对象，有两个引用路径，一个是来自SoftReference对象的软引用，一个来自变量aRef的强引用，所以这个MyObject对象是强可及对象。

我们可以结束aReference对这个MyObject实例的强引用:   aRef = null;

这个MyObject对象成为了软引用对象。如果垃圾收集线程进行内存垃圾收集，并不会因为有一个SoftReference对该对象的引用而始终保留该对象。

垃圾收集线程会在虚拟机抛出OutOfMemoryError之前回收软可及对象，而且虚拟机会尽可能优先回收长时间闲置不用的软可及对象，对那些刚刚构建的或刚刚使用过的“新”软可反对象会被虚拟机尽可能保留。

 

在回收这些对象之前，我们可以通过:   MyObject anotherRef=(MyObject)aSoftRef.get();  

重新获得对该实例的强引用。而回收之后，调用get()方法就只能得到null了。但这个SoftReference对象已经不再具有存在的价值，需要一个适当的清除机制，避免大量SoftReference对象带来的内存泄漏。

在java.lang.ref包里还提供了ReferenceQueue。如果在创建SoftReference对象的时候，使用了一个ReferenceQueue对象作为参数提供给SoftReference的构造方法，如:

ReferenceQueue queue = new  ReferenceQueue();  

SoftReference  ref=new  SoftReference(aMyObject, queue);  

那么当这个SoftReference所软引用的aMyOhject被垃圾收集器回收的同时，ref所强引用的SoftReference对象被列入ReferenceQueue。

利用这个方法，我们可以检查哪个SoftReference所软引用的对象已经被回收。于是我们可以把这些失去所软引用的对象的SoftReference对象清除掉。常用的方式为:

SoftReference ref = null;  

while ((ref = (EmployeeRef) q.poll()) != null) {  

​    // 清除ref  

}  

 

 

SoftReference:通过该类引用后的对象仅在虚拟机的内存不足的时候才会被回收,多用于高速缓存.

WeakReference:该类不会妨碍GC对对象的正常回收.只具有弱引用的对象拥有更短暂的生命周期。在垃圾回收器线程扫描它所管辖的内存区域的过程中，一旦发现了只具有弱引用的对象，不管当前内存空间足够与否，都会回收它的内存。不过，由于垃圾回收器是一个优先级很低的线程，因此不一定会很快发现那些只具有弱引用的对象。

 

例子：

public class A {

​    public String name;

​    protected void finalize() throws Throwable {

​        System.out.println("Finalize");

​    }

}

public static void main(String[] args) throws InterruptedException {

​    A a = new A();

​    a.name = "kutear";

​    SoftReference<A> softReference = new SoftReference<A>(a);

​    a = null;    //softReference不会被立即回收，仅在内存不足时才会回收

​    System.out.println(softReference.get().name);

​    int i = 0;

 

​    while (softReference.get() != null) {

​        if (i == 10) {

​            System.gc();

​            System.out.println("GC");

​        }

​        Thread.sleep(1000);

​        System.out.println(i);

​        i++;

​    }

​    System.out.println("Finish");

}

 

结果：

kutear

0

1

2

3

4

5

6

7

8

9

GC

10

11

。。。。。。。  到无穷

 

 

 

 

public static void main(String[] args) throws InterruptedException {

​    A a = new A();

​    a.name = "kutear";

​    WeakReference<A> weakReference = new WeakReference<A>(a);

​    a = null;

​    System.out.println(weakReference.get().name);

​    int i = 0;

 

​    while (weakReference.get() != null) {

​        if (i == 10) {

​            System.gc();

​            System.out.println("GC");

​        }

​        Thread.sleep(1000);

​        System.out.println(i);

​        i++;

​    }

​    System.out.println("Finish");

}

结果：

kutear

0

1

2

3

4

5

6

7

8

9

GC

Finalize

10

Finish

 

例子2：

public class test {  

​    public static void main(String[] args) {  

​        WeakReference<People>reference=new WeakReference<People>(new People("zhouqian",20));  

​        System.out.println(reference.get());  

​        System.gc();//通知GVM回收资源  

​        System.out.println(reference.get());  

​    }  

}  

class People{  

​    public String name;  

​    public int age;  

​    public People(String name,int age) {  

​        this.name=name;  

​        this.age=age;  

​    }  

​    @Override  

​    public String toString() {  

​        return "[name:"+name+",age:"+age+"]";  

​    }  

}  

结果：

[name:zhouqian,age:20]

null

 

 

 

public class test {  

​    public static void main(String[] args) {  

​        People people=new People("zhouqian",20);  

​        WeakReference<People>reference=new WeakReference<People>(people);//<span style="color:#FF0000;">关联强引用</span>  

​        System.out.println(reference.get());  

​        System.gc();  

​        System.out.println(reference.get());  

​    }  

}  

class People{  

​    public String name;  

​    public int age;  

​    public People(String name,int age) {  

​        this.name=name;  

​        this.age=age;  

​    }  

​    @Override  

​    public String toString() {  

​        return "[name:"+name+",age:"+age+"]";  

​    }  

}//结果发生了很大的变化  

[name:zhouqian,age:20]  

[name:zhouqian,age:20]  

 

 

4.虚引用（PhantomReference）

虚引用和前面的软引用、弱引用不同，它并不影响对象的生命周期。在java中用java.lang.ref.PhantomReference类表示。如果一个对象与虚引用关联，则跟没有引用与之关联一样，在任何时候都可能被垃圾回收器回收。

要注意的是，虚引用必须和引用队列关联使用，当垃圾回收器准备回收一个对象时，如果发现它还有虚引用，就会把这个虚引用加入到与之 关联的引用队列中。程序可以通过判断引用队列中是否已经加入了虚引用，来了解被引用的对象是否将要被垃圾回收。如果程序发现某个虚引用已经被加入到引用队列，那么就可以在所引用的对象的内存被回收之前采取必要的行动。

public class Main {  

​    public static void main(String[] args) {  

​        ReferenceQueue<String> queue = new ReferenceQueue<String>();  

​        PhantomReference<String> pr = new PhantomReference<String>(new String("hello"), queue);  

​        System.out.println(pr.get());  

​    }  

}  

 

 

 

使用得最多的就是软引用和弱引用

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

1.那么到底如何利用它们来优化程序性能，从而避免OOM的问题呢？

下面举个例子，假如有一个应用需要读取大量的本地图片，如果每次读取图片都从硬盘读取，则会严重影响性能，但是如果全部加载到内存当中，又有可能造成内存溢出，此时使用软引用可以解决这个问题。

设计思路是：用一个HashMap来保存图片的路径 和 相应图片对象关联的软引用之间的映射关系，在内存不足时，JVM会自动回收这些缓存图片对象所占用的空间，从而有效地避免了OOM的问题。

2.使用软引用构建敏感数据的缓存

 

 

 

如何利用软引用和弱引用解决OOM问题

　　前面讲了关于软引用和弱引用相关的基础知识，那么到底如何利用它们来优化程序性能，从而避免OOM的问题呢？

　　下面举个例子，假如有一个应用需要读取大量的本地图片，如果每次读取图片都从硬盘读取，则会严重影响性能，但是如果全部加载到内存当中，又有可能造成内存溢出，此时使用软引用可以解决这个问题。

　　设计思路是：用一个HashMap来保存图片的路径 和 相应图片对象关联的软引用之间的映射关系，在内存不足时，JVM会自动回收这些缓存图片对象所占用的空间，从而有效地避免了OOM的问题。在Android开发中对于大量图片下载会经常用到。

 

 

 

 

 

=======================================================================JAVA FinalReference=======================================================================

Java开发不必关心内存的释放、申请和垃圾回收，这些事情都有JVM代劳，但是JVM依然提供了一些方式，让我们能够在应用的层次利用内存或者GC特性，从而更好的使用内存。Reference(引用)就是其中一种。

 

StrongReference（强引用）

我们平时开发中new一个对象出来，这种引用便是强引用。 JVM 系统采用 Finalizer 来管理每个强引用对象 , 并将其被标记要清理时加入 ReferenceQueue, 并逐一调用该对象的 finalize() 方法。

SoftReference（软引用）

当内存足够的时候，软引用所指向的对象没有其他强引用指向的话，GC的时候并不会被回收，当且只当内存不够时才会被GC回收（调用finalize方法）。强度仅次于强引用。

WeakReference（弱引用）

弱引用指向的对象没有任何强引用指向的话，GC的时候会进行回收。

PhantomReference（虚引用）

如果一个对象仅持有虚引用，那么它就和没有任何引用一样，在任何时候都可能被垃圾回收器回收。

 

 

https://blog.csdn.net/myjcxd/article/details/68943044

 

 

 

=======================================================================降低Java垃圾回收开销的5条建议=======================================================================

1: 预测集合的容量

 

2: 直接处理数据流

 

当处理数据流时，比如从一个文件读取数据或者从网络中下载数据，下面的代码是非常常见的：

byte[] fileData = readFileToByteArray(new File("myfile.txt"));

所产生的字节数组可能被解析 XML 文档、JSON 对象或者协议缓冲消息，以及一些常见的可选项。

当处理大文件或者文件的大小无法预测时，上面的做法很是不明智的，因为当 JVM 无法分配一个缓冲区来处理真正文件时，就会导致OutOfMemeoryErrors。

即使数据的大小是可管理的，当到垃圾回收时，使用上面的模式依然会造成巨大的开销，因为它在堆中分配了一块非常大的区域来存储文件数据。

一种更加好的处理方式是使用合适的 InputStream (比如在这个例子中使用 FileInputStream)直接传递给解析器，不再一次性将整个文件读取到一个字节数组中。所有主流的开源库都提供相应的 API 来直接接受一个输入流进行处理,比如:

FileInputStream fis = new FileInputStream(fileName);

MyProtoBufMessage msg = MyProtoBufMessage.parseFrom(fis);

 

3: 使用不可变的对象

 

 

=======================================================================JAVA不可变类(immutable)机制与String的不可变性=======================================================================

不可变对象，顾名思义就是创建后不可以改变的对象，典型的例子就是Java中的String类。

 

 

final 修饰的对象 只是不能指向其他对象而已， 对象本身还是可修改的

不可变类:

不可变类：所谓的不可变类是指这个类的实例一旦创建完成后，就不能改变其成员变量值。如JDK内部自带的很多不可变类：Interger、Long和String等。

可变类：相对于不可变类，可变类创建实例后可以改变其成员变量值，开发中创建的大部分类都属于可变类。

 

不可变类优点:

线程安全

不可变对象是线程安全的，在线程之间可以相互共享，不需要利用特殊机制来保证同步问题，因为对象的值无法改变。可以降低并发错误的可能性，因为不需要用一些锁机制等保证内存一致性问题也减少了同步开销。

 

 

\1. 类添加final修饰符，保证类不被继承。

 

2.通过构造器初始化所有成员，进行深拷贝(deep copy)

如果构造器传入的对象直接赋值给成员变量，还是可以通过对传入对象的修改进而导致改变内部变量的值。例如：

 

public final class ImmutableDemo {  

​    private final int[] myArray;  

​    public ImmutableDemo(int[] array) {  

​        this.myArray = array; // wrong  

​    }  

}

这种方式不能保证不可变性，myArray和array指向同一块内存地址，用户可以在ImmutableDemo之外通过修改array对象的值来改变myArray内部的值。

为了保证内部的值不被修改，可以采用深度copy来创建一个新内存保存传入的值。正确做法：

public final class MyImmutableDemo {  

​    private final int[] myArray;  

​    public MyImmutableDemo(int[] array) {  

​        this.myArray = array.clone();   

​    }   

}

 

\5. 在getter方法中，不要直接返回对象本身，而是克隆对象，并返回对象的拷贝

这种做法也是防止对象外泄，防止通过getter获得内部可变成员对象后对成员变量直接操作，导致成员变量发生改变。

 

 

 

String对象的不可变性：

public final class String

​    implements java.io.Serializable, Comparable<String>, CharSequence

{

​    /** The value is used for character storage. */

​    private final char value[];

​    /** The offset is the first index of the storage that is used. */

​    private final int offset;

​    /** The count is the number of characters in the String. */

​    private final int count;

​    /** Cache the hash code for the string */

​    private int hash; // Default to 0

​    ....

​    public String(char value[]) {

​         this.value = Arrays.copyOf(value, value.length); // deep copy操作

​     }

​    ...

​     public char[] toCharArray() {

​     // Cannot use Arrays.copyOf because of class initialization order issues

​        char result[] = new char[value.length];

​        System.arraycopy(value, 0, result, 0, value.length);

​        return result;

​    }

​    ...

}

如上代码所示，可以观察到以下设计细节:

 

String类被final修饰，不可继承

string内部所有成员都设置为私有变量

不存在value的setter

并将value和offset设置为final。

当传入可变数组value[]时，进行copy而不是直接将value[]复制给内部变量.

获取value时不是直接返回对象引用，而是返回对象的copy.

这都符合上面总结的不变类型的特性，也保证了String类型是不可变的类。

 

线程安全考虑。

同一个字符串实例可以被多个线程共享。这样便不用因为线程安全问题而使用同步。字符串自己便是线程安全的。

！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！

\4. 支持hash映射和缓存。

因为字符串是不可变的，所以在它创建的时候hashcode就被缓存了，不需要重新计算。这就使得字符串很适合作为Map中的键，字符串的处理速度要快过其它的键对象。这就是HashMap中的键往往都使用字符串。

！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！

 

String 对象不可变的（immutable）。分析为什么要这么设计，可能有以下3个原因：

String pool：这是方法（method）区域里一个特殊的存储区域，创建一个 String 时，如果已经在 String pool 中存在，那么会返回已存在的 String 引用。

允许 String 缓存 hashcode：String 定义中，有 hash 成员变量 private int hash; // 默认为0，对 hashcode 进行缓存。

安全性：确保不会被恶意篡改。

 

1 String str="abc";

2 System.out.println(str);

3 str=str+"de";

4 System.out.println(str);

如果运行这段代码会发现先输出“abc”，然后又输出“abcde”，好像是str这个对象被更改了，其实，这只是一种假象罢了，JVM对于这几行代码是这样处理的，首先创建一个String对象str，并把“abc”赋值给str，然后在第三行中，其实JVM又创建了一个新的对象也名为str，然后再把原来的str的值和“de”加起来再赋值给新的str，而原来的str就会被JVM的垃圾回收机制（GC）给回收掉了，所以，str实际上并没有被更改，也就是前面说的String对象一旦创建之后就不可更改了。所以，Java中对String对象进行的操作实际上是一个不断创建新的对象并且将旧的对象回收的一个过程，所以执行速度很慢。

而StringBuilder和StringBuffer的对象是变量，对变量进行操作就是直接对该对象进行更改，而不进行创建和回收的操作，所以速度要比String快很多。

 

StringBuffer中很多方法可以带有synchronized关键字，所以可以保证线程是安全的，但StringBuilder的方法则没有该关键字，所以不能保证线程安全

public synchronized StringBuffer append(String str) {

​    super.append(str);

​    return this;

}

 

 

得到的经验：

String.class  :

public String(StringBuffer buffer) {

​    synchronized(buffer) {

​        this.value = Arrays.copyOf(buffer.getValue(), buffer.length());

​    }

}

StringBuffer 是线程安全的，指的是 StringBuffer 有一些方法是线程安全的， 但是多线程操作StringBuffer本身，还是要加锁的。

类似于 ConcurrentHashMap ，ConcurrentHashMap 的 set、get 是线程安全的，但是操作 ConcurrentHashMap本身，还是要加锁的。

 

StringBuffer：

public synchronized StringBuffer append(CharSequence s, int start, int end)

{

​    super.append(s, start, end);

​    return this;

}

public synchronized StringBuffer append(char[] str) {

​    super.append(str);

​    return this;

}

 

String对象的是否真的不可变?

虽然String对象将value设置为final,并且还通过各种机制保证其成员变量不可改变。但是还是可以通过反射机制的手段改变其值。例如：

 

​    //创建字符串"Hello World"， 并赋给引用s

​    String s = "Hello World";

​    System.out.println("s = " + s); //Hello World

 

​    //获取String类中的value字段

​    Field valueFieldOfString = String.class.getDeclaredField("value");

​    //改变value属性的访问权限

​    valueFieldOfString.setAccessible(true);

 

​    //获取s对象上的value属性的值

​    char[] value = (char[]) valueFieldOfString.get(s);

​    //改变value所引用的数组中的第5个字符

​    value[5] = '_';

​    System.out.println("s = " + s);  //Hello_World

打印结果为：

 

s = Hello World

s = Hello_World

 

发现String的值已经发生了改变。也就是说，通过反射是可以修改所谓的“不可变”对象的

 

字符串常量池(String pool, String intern pool, String保留池) 是Java堆内存中一个特殊的存储区域, 当创建一个String对象时,假如此字符串值已经存在于常量池中,则不会创建一个新的对象,而是引用已经存在的对象。

 

如下面的代码所示,将会在堆内存中只创建一个实际String对象.

String s1 = "abcd";

String s2 = "abcd";

 

 

允许String对象缓存HashCode

Java中String对象的哈希码被频繁地使用, 比如在hashMap 等容器中。

字符串不变性保证了hash码的唯一性,因此可以放心地进行缓存.这也是一种性能优化手段,意味着不必每次都去计算新的哈希码. 在String类的定义中有如下代码:

private int hash;//用来缓存HashCode

 

 

 

String字面量可以通过’==’判断两个字符串是否相同，是因为大家都知道’==’是用来判断两个对象的值引用地址是否一致，两个值一样的字符串字面量定义是否指向同一个值内存地址呢？答案是肯定的。

 

public class ConstPoolTest {

​    public static void main(String[] args){

​        String str1 = "strVal_1";

​        String str2 = "strVal_1";

​        //print str1==str2 is true

​        System.out.printf("str1==str2 is %b",str1==str2);

​    }

}

true

 

 

String str1 = "strVal_1";

String str2 = new String("strVal_1");

System.out.printf("str1==str2 is %b",str1==str2);

false

 

String s = new String(“xyz”); 创建了几个字符串对象？

两个对象，一个静态存储区“xyz”, 一个用new创建在堆上的对象。

 

String str1 = "abcdef";

String str2 = "abc"+"def";

System.out.printf("str1==str2 is %b",str1==str2);

true

 

 

总的说，String 有个特点： 如果程序中有多个String对象，都包含相同的字符串序列，那么这些String对象都映射到同一块内存区域，所以两次new String(“hello”)生成的两个实例，虽然是相互独立的，但是对它们使用hashCode()应该是同样的结果。Note: 字符串数组并非这样，只有String是这样。即hashCode对于String，是基于其内容的。

 

public class StringHashCode {

​       public static void main(String[] args) {

​            \\输出结果相同

​            String[] hellos = "Hello Hello".split(" " );

​            System.out.println(""+hellos[0].hashCode());

​            System.out.println(""+hellos[1].hashCode());

​            \\输出结果相同

​            String a = new String("hello");

​            String b = new String("hello");

​            System.out.println(""+a.hashCode());

​            System.out.println(""+b.hashCode());

​      }

}

 

 

EG:

String s1 = "Cat";

String s2 = "Cat";

String s3 = new String("Cat");

System.out.println("s1 == s2 :"+(s1==s2));

System.out.println("s1 == s3 :"+(s1==s3));

答案：

s1 == s2 :true

s1 == s3 :false

理解 String pool，s1 与 s2 字符串内容相同，因此直接从 String pool 中返回相同的地址。s3 会创建一个新的 String 对象，因此 s1==s3 结果返回 false。

 

 

String s3 = new String(“Cat”) 这句代码会创建几个 String 对象？

答案：1 或 2 个。

考点：理解 String pool 机制。如果 Spring pool 在执行语句之前没有 “Cat” 对象，那么会创建 2 个 String；反之只创建 1 个 String 对象，”Cat” 会从 String pool 中直接返回对象。

 

 

如何比较两个字符串？使用 “==” 还是 equals() 方法？

答案：简单来讲，“==” 测试的是两个对象的引用是否相同，而equals()比较的是两个字符串的值是否相等。除非你想检查的是两个字符串是否是同一个对象，否则你应该使用 equals() 来比较字符串。

String s1 = "Cat";

String s3 = new String("Cat");

System.out.println("s1 == s3 :"+(s1==s3));

System.out.println("s1.equals(s3) :"+(s1.equals(s3)));

结果：

s1 == s3 :false

s1.equals(s3) :true

 

注意：

String s3 = new String("Cat");  会在堆中新建一个对象，这个对象是实在的对象 "Cat",不会指向方法区。

 

例子：

String str1 = "str";

String str2 = "ing";

String str3 = "str" + "ing";//常量池中的对象

String str4 = str1 + str2; //在堆上创建的新的对象    

String str5 = "string";//常量池中的对象

System.out.println(str3 == str4);//false

System.out.println(str3 == str5);//true

System.out.println(str4 == str5);//false

 

 

为什么针对安全保密高的信息，char[] 比 String 更好?

答案：因为String是不可变的，就是说它一旦创建，就不能更改了，直到垃圾收集器将它回收。而字符数组中的元素是可以更改的，这就意味着你可以在使用完之后将其更改，而不会保留原始数据。所以使用字符数组的话，安全保密性高的信息，如密码之类信息，将不会存在于系统中被他人看到。

 

 

字符串池之所以可能，就是因为字符串在 Java 中是不可变的。由此 Java 运行时环境节省了大量堆空间，因为不同的 String 变量可以引用池中的同一 String 变量。如果 String 不是不可变的, 则字符串驻留（String interning）将是不可能的，因为一旦任一变量更改所引用的String对象的值，它也会反映在其他变量中。

如果字符串不是不可变的，那么它可能会对应用程序造成严重的安全威胁。例如，数据库用户名和密码都作为 String 传递以获取数据库连接，Socket 编程的主机和端口信息也是如此。由于字符串是不可变的，因此其值不能被更改。否则，任何黑客都可以篡改其引用的值，这会导致应用程序中的安全问题。

由于 String 是不可变的，因此它对与多线程处理来说是安全的，并且可以在不同的线程之间共享单个 String 实例。这避免了为线程安全使用同步；字符串是隐式线程安全的。

字符串被用在 Java 类加载器中，其不可变性为类加载器加载正确的类提供了安全性。否则的话，请考虑这样一个危险的情况，在你尝试加载 java.sql.Connection 类时，你引用的值却被更改为 myhacked.Connection，并且它能对数据库执行你不需要的操作。

由于 String 是不可变的，因此在它被创建时其散列码就被缓存，不需要再次计算。这使得它成为映射中键的理想对象，它的处理速度比其他HashMap 键类型快。这就是为什么 String 是 HashMap 中最常用的键类型。

 

 

 

 

new String()究竟创建几个对象?

new String("hello")这样的创建方式，到底创建了几个String对象？

这个有参构造函数的源码则是这样的public String(String original)，这就是说，我们可以把代码转换为下面这种：

String temp = "hello";  // 在常量池中

String str = new String(temp); // 在堆上

 

这段代码就创建了2个String对象，temp指向在常量池中的，str指向堆上的，而str内部的char value[]则指向常量池中的char value[]，所以这里的答案是2个对象。

那之前我为什么说答案是1个的也对呢，假如就只有这一句String str = new String("hello")代码，并且此时的常量池的没有"hello"这个String，那么答案是两个;如果此时常量池中，已经存在了"hello"，那么此时就只创建堆上str，而不会创建常量池中temp,(注意这里都是引用)，所以此时答案就是1个。

 

 

 

​    

！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！

=======================================================================Callable和DeferredResult=======================================================================

DeferredResult和Callable都是为了异步生成返回值提供基本的支持。

简单来说就是一个请求进来，如果你使用了DeferredResult或者Callable，在没有得到返回数据之前，

DispatcherServlet和所有Filter就会退出Servlet容器线程，但响应保持打开状态，一旦返回数据有了，

这个DispatcherServlet就会被再次调用并且处理，以异步产生的方式，向请求端返回值。

这么做的好处就是请求不会长时间占用服务连接池，提高服务器的吞吐量。

 

 

 

 

 

 

我的心得：

异步 既可以 是 浏览器， 也可以是 服务器端。

Servlet 3中的异步支持为在另一个线程中处理HTTP请求提供了可能性。当有一个长时间运行的任务时，这是特别有趣的，因为当另一个线程处理这个请求时，容器线程被释放，并且可以继续为其他请求服务

 

 

站在一定高度来看这问题，Callable和Deferredresult做的是同样的事情——释放容器线程，在另一个线程上异步运行长时间的任务。不同的是谁管理执行任务的线程。

 

Spring MVC的使用——DefferedResult：

 

要使用Spring MVC的异步功能，你得先确保你用的是Servlet 3.0或以上的版本，Maven中如此配置：

<dependency>

  <groupId>javax.servlet</groupId>

  <artifactId>javax.servlet-api</artifactId>

  <version>3.1.0</version>

  <scope>provided</scope>

</dependency>

<dependency>

  <groupId>org.springframework</groupId>

  <artifactId>spring-webmvc</artifactId>

  <version>4.2.3.RELEASE</version>

</dependency>

 

传统的同步模式的Controller是返回ModelAndView，而异步模式则是返回DeferredResult<ModelAndView>。

 

@RequestMapping(value="/asynctask", method = RequestMethod.GET)

public DeferredResult<ModelAndView> asyncTask(){

​    DeferredResult<ModelAndView> deferredResult = new DeferredResult<ModelAndView>();

​    System.out.println("/asynctask 调用！thread id is : " + Thread.currentThread().getId());

​    longTimeAsyncCallService.makeRemoteCallAndUnknownWhenFinish(new LongTermTaskCallback() {

​        @Override

​        public void callback(Object result) {

​            System.out.println("异步调用执行完成, thread id is : " + Thread.currentThread().getId());

​            ModelAndView mav = new ModelAndView("remotecalltask");

​            mav.addObject("result", result);

​            deferredResult.setResult(mav);

​        }

​    });

}

longTimeAsyncCallService是我写的一个模拟长时间异步调用的服务类，调用之，立即返回，当它处理完成时候，就钩起一个线程调用我们提供的回调函数，这跟“图3”描述的一样，它的代码如下：

public interface LongTermTaskCallback {

​    void callback(Object result);

}

public class LongTimeAsyncCallService {

​    private final int CorePoolSize = 4;

​    private final int NeedSeconds = 3;

​    private Random random = new Random();

​    private ScheduledExecutorService scheduler = Executors.newScheduledThreadPool(CorePoolSize);

​    public void makeRemoteCallAndUnknownWhenFinish(LongTermTaskCallback callback){

​        System.out.println("完成此任务需要 : " + NeedSeconds + " 秒");

​        scheduler.schedule(new Runnable() {

​            @Override

​            public void run() {

​                callback.callback("长时间异步调用完成.");

​            }

​        }, "这是处理结果:)", TimeUnit.SECONDS);

​    }

}

输出的结果是：

 

/asynctask 调用！thread id is : 46

完成此任务需要 : 3 秒

异步调用执行完成, thread id is : 47

 

由此可见返回结果的线程和请求处理线程不是同一线程。

 

 

还有个叫WebAsyncTask

返回DefferedResult<ModelAndView>并非唯一做法，还可以返回WebAsyncTask来实现“异步”，但略有不同，不同之处在于返回WebAsyncTask的话是不需要我们主动去调用Callback的，看例子：

 

@RequestMapping(value="/longtimetask", method = RequestMethod.GET)

public WebAsyncTask longTimeTask(){

​    System.out.println("/longtimetask被调用 thread id is : " + Thread.currentThread().getId());

​    Callable<ModelAndView> callable = new Callable<ModelAndView>() {

​        public ModelAndView call() throws Exception {

​            Thread.sleep(3000); //假设是一些长时间任务

​            ModelAndView mav = new ModelAndView("longtimetask");

​            mav.addObject("result", "执行成功");

​            System.out.println("执行成功 thread id is : " + Thread.currentThread().getId());

​            return mav;

​        }

​    };

​    return new WebAsyncTask(callable);

}

其核心是一个Callable<ModelAndView>，事实上，直接返回Callable<ModelAndView>都是可以的，但我们这里包装了一层，以便做后面提到的“超时处理”。和前一个方案的差别在于这个Callable的call方法并不是我们直接调用的，而是在longTimeTask返回后，由Spring MVC用一个工作线程来调用，执行，打印出来的结果：

 

/longtimetask被调用 thread id is : 56

执行成功 thread id is : 57

 

 

处理超时:

如果“长时间处理任务”一直没返回，那我们也不应该让客户端无限等下去啊，总归要弄个“超时”出来。如图：

其实“超时处理线程”和“回调处理线程”可能都是线程池中的某个线程，我为了清晰点把它们分开画而已。增加这个超时处理在Spring MVC中非常简单，先拿WebAsyncTask那段代码来改一下：

 

@RequestMapping(value="/longtimetask", method = RequestMethod.GET)

public WebAsyncTask longTimeTask(){

​    System.out.println("/longtimetask被调用 thread id is : " + Thread.currentThread().getId());

​    Callable<ModelAndView> callable = new Callable<ModelAndView>() {

​        public ModelAndView call() throws Exception {

​            Thread.sleep(3000); //假设是一些长时间任务

​            ModelAndView mav = new ModelAndView("longtimetask");

​            mav.addObject("result", "执行成功");

​            System.out.println("执行成功 thread id is : " + Thread.currentThread().getId());

​            return mav;

​        }

​    };

​    WebAsyncTask asyncTask = new WebAsyncTask(2000, callable);

​    asyncTask.onTimeout(

​            new Callable<ModelAndView>() {

​                public ModelAndView call() throws Exception {

​                    ModelAndView mav = new ModelAndView("longtimetask");

​                    mav.addObject("result", "执行超时");

​                    System.out.println("执行超时 thread id is ：" + Thread.currentThread().getId());

​                    return mav;

​                }

​            }

​    );

​    return new WebAsyncTask(3000, callable);

}

注意看红色字体部分代码，这就是前面提到的为什么Callable还要外包一层的缘故，给WebAsyncTask设置一个超时回调，即可实现超时处理，在这个例子中，正常处理需要3秒钟，而超时设置为2秒，所以肯定会出现超时，执行打印log如下：

 

/longtimetask被调用 thread id is : 59

执行超时 thread id is ：61

执行成功 thread id is : 80

 

嗯？明明超时了，怎么还会“执行成功”呢？超时归超时，超时并不会打断正常执行流程，但注意，出现超时后我们给客户端返回了“超时”的结果，那接下来即便正常处理流程成功，客户端也收不到正常处理成功所产生的结果了，这带来的问题就是：客户端看到了“超时”，实际上操作到底有没有成功，客户端并不知道，但通常这也不是什么大问题，因为用户在浏览器上再刷新一下就好了。:D

 

好，再来看DefferedResult方式的超时处理：

 

@RequestMapping(value = "/asynctask", method = RequestMethod.GET)

​    public DeferredResult<ModelAndView> asyncTask() {

​        DeferredResult<ModelAndView> deferredResult = new DeferredResult<ModelAndView>(2000L);

​        System.out.println("/asynctask 调用！thread id is : " + Thread.currentThread().getId());

​        longTimeAsyncCallService.makeRemoteCallAndUnknownWhenFinish(new LongTermTaskCallback() {

​            @Override

​            public void callback(Object result) {

​                System.out.println("异步调用执行完成, thread id is : " + Thread.currentThread().getId());

​                ModelAndView mav = new ModelAndView("remotecalltask");

​                mav.addObject("result", result);

​                deferredResult.setResult(mav);

​            }

​        });

​        deferredResult.onTimeout(new Runnable() {

​            @Override

​            public void run() {

​                System.out.println("异步调用执行超时！thread id is : " + Thread.currentThread().getId());

​                ModelAndView mav = new ModelAndView("remotecalltask");

​                mav.addObject("result", "异步调用执行超时");

​                deferredResult.setResult(mav);

​            }

​        });

​        return deferredResult;

​    }

非常类似，对吧，我把超时设置为2秒，而正常处理需要3秒，一定会超时，执行结果如下：

 

/asynctask 调用！thread id is : 48

完成此任务需要 : 3 秒

异步调用执行超时！thread id is : 51

异步调用执行完成, thread id is : 49

 

异常处理

貌似没什么差别，在Controller中的处理和之前同步模式的处理是一样一样的：

 

@ExceptionHandler(Exception.class)

​    public ModelAndView handleAllException(Exception ex) {

​        ModelAndView model = new ModelAndView("error");

​        model.addObject("result", ex.getMessage());

​        return model;

}

 

 

DeferredResult的处理顺序与Callable十分相似,由应用程序多线程产生异步结果:

1.Controller返回一个DeferredResult对象,并且把它保存在内在队列当中或者可以访问它的列表中。

2.Spring MVC开始异步处理.

3.DispatcherServlet与所有的Filter的Servlet容器线程退出,但Response仍然开放。

4.application通过多线程返回DeferredResult中sets值.并且Spring MVC分发request给Servlet容器.

5.DispatcherServlet再次被调用并且继续异步的处理产生的结果.

 

 

=======================================================================ArrayList 的 removeAll 源码 =======================================================================

 

 

 

 

=======================================================================集合的交集，并集，差集=======================================================================

Set<String> set1 = new HashSet<>();

Set<String> set2 = new HashSet<>();

set1.add("a");

set1.add("b");

set1.add("c");

set2.add("c");

set2.add("d");

set2.add("e");

//交集

set1.retainAll(set2);

System.out.println("交集是 "+set1);     "c"

 

并集

set1.addAll(set2);

 

差集

set1.removeAll(set2);    [a,b]

 

 

=======================================================================Atomic=======================================================================

AtomicBoolean：原子更新布尔类型。

AtomicInteger：原子更新整型。

AtomicLong：原子更新长整型。

 

原子更新数组类:

AtomicIntegerArray：原子更新整型数组里的元素。

AtomicLongArray：原子更新长整型数组里的元素。

AtomicReferenceArray：原子更新引用类型数组里的元素。

 

AtomicIntegerArray类主要是提供原子的方式更新数组里的整型，其常用方法如下:

int addAndGet(int i, int delta)：以原子方式将输入值与数组中索引i的元素相加。

boolean compareAndSet(int i, int expect, int update)：如果当前值等于预期值，则以原子方式将数组位置i的元素设置成update值.

 

public class AtomicIntegerArrayTest {

 

​    static int[] value = new int[] { 1, 2 };

 

​    static AtomicIntegerArray ai = new AtomicIntegerArray(value);

 

​    public static void main(String[] args) {

​        ai.getAndSet(0, 3);

​        System.out.println(ai.get(0));

​                System.out.println(value[0]);

​    }

 

}

输出:

3

1

 

AtomicIntegerArray类需要注意的是，数组value通过构造方法传递进去，然后AtomicIntegerArray会将当前数组复制一份，所以当AtomicIntegerArray对内部的数组元素进行修改时，不会影响到传入的数组。

 

 

原子更新字段类:

AtomicIntegerFieldUpdater：原子更新整型的字段的更新器。

AtomicLongFieldUpdater：原子更新长整型字段的更新器。

AtomicStampedReference：原子更新带有版本号的引用类型。该类将整数值与引用关联起来，可用于原子的更数据和数据的版本号，可以解决使用CAS进行原子更新时，可能出现的ABA问题。

 

public class AtomicIntegerFieldUpdaterTest {

​    private static AtomicIntegerFieldUpdater<User> a = AtomicIntegerFieldUpdater

​            .newUpdater(User.class, "old");

​    public static void main(String[] args) {

​        User conan = new User("conan", 10);

​        System.out.println(a.getAndIncrement(conan));

​        System.out.println(a.get(conan));

​    }

​    public static class User {

​        private String name;

​        public volatile int old;

​        public User(String name, int old) {

​            this.name = name;

​            this.old = old;

​        }

​        public String getName() {

​            return name;

​        }

​        public int getOld() {

​            return old;

​        }

​    }

}

 

10

11

 

 

=======================================================================文件路径=======================================================================

 

http://www.importnew.com/20943.html

 

 

================================================================java提高篇之集合大家族================================================================

http://www.importnew.com/20894.html

 

每一个ArrayList都有一个初始容量（10）

 

HashSet

HashSet堪称查询速度最快的集合，因为其内部是以HashCode来实现的。它内部元素的顺序是由哈希码来决定的，所以它不保证set 的迭代顺序；特别是它不保证该顺序恒久不变。

 

Queue

队列，它主要分为两大类，一类是阻塞式队列，队列满了以后再插入元素则会抛出异常，主要包括ArrayBlockQueue、PriorityBlockingQueue、LinkedBlockingQueue。另一种队列则是双端队列，支持在头、尾两端插入和移除元素，主要包括：ArrayDeque、LinkedBlockingDeque、LinkedList。

 

 

 

阻塞栈：

import java.util.concurrent.BlockingDeque;

import java.util.concurrent.LinkedBlockingDeque;

public class BlockingDequeTest {

​    public static void main(String[] args) throws InterruptedException {

​            BlockingDeque<String> bDeque = new LinkedBlockingDeque<String>(20);

​            for (int i = 0; i < 30; i++) {

​                //将指定元素添加到此阻塞栈中

​                bDeque.putFirst("" + i);

​                System.out.println("向阻塞栈中添加了元素:" + i);

​            }

​            System.out.println("程序到此运行结束，即将退出----");

​    }

}

 

import java.util.concurrent.BlockingDeque;

import java.util.concurrent.LinkedBlockingDeque;

public class BlockingDequeTest {

​    public static void main(String[] args) throws InterruptedException {

​            BlockingDeque<String> bDeque = new LinkedBlockingDeque<String>(20);

​            for (int i = 0; i < 30; i++) {

​                //将指定元素添加到此阻塞栈中

​                bDeque.putFirst("" + i);

​                System.out.println("向阻塞栈中添加了元素:" + i);

​                if(i > 18){

​                    //从阻塞栈中取出栈顶元素，并将其移出

​                    System.out.println("从阻塞栈中移出了元素：" + bDeque.pollFirst());

​                }

​            }

​            System.out.println("程序到此运行结束，即将退出----");

​    }

}

 

================================================================final================================================================

final方法 ： 父类的final方法是不能被子类所覆盖的

final类 ：  该类是最终类，它不希望也不允许其他来继承它

final参数 ：

​        同final修饰参数在内部类中是非常有用的，在匿名内部类中，为了保持参数的一致性，若所在的方法的形参需要被内部类里面使用时，该形参必须为final。

 

 

 

================================================================volatile  happens before规则==============================================

把对volatile变量的单个读/写，看成是使用同一个监视器锁对这些单个读/写操作做了同步。

对一个volatile变量的读，总是能看到（任意线程）对这个volatile变量最后的写入。

如果是多个volatile操作或类似于volatile++这种复合操作，这些操作整体上不具有原子性。

 

volatile变量规则：对一个volatile域的写，happens-before于任意后续对这个volatile域的读。

传递性：如果A happens-before B，且B happens-before C，那么A happens-before C。

 

class VolatileExample {

​    int a = 0;

​    volatile boolean flag = false;

​    public void writer() {

​        a = 1;                   //1

​        flag = true;               //2

​    }

​    public void reader() {

​        if (flag) {                //3

​            int i =  a;           //4

​            ……

​        }

​    }

}

 

1.根据程序次序规则，1 happens before 2; 3 happens before 4。

2.根据volatile规则，2 happens before 3。

3.根据happens before 的传递性规则，1 happens before 4。  ！！！！！！！！！！！！！！！！！！！！！！！！！

 

！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！

这里A线程写一个volatile变量后，B线程读同一个volatile变量。A线程在写volatile变量之前所有可见的共享变量，在B线程读同一个volatile变量后，将立即变得对B线程可见。

 

 

 

happens-before:

程序顺序规则：一个线程中的每个操作，happens-before于该线程中的任意后续操作。

监视器锁规则：对一个锁的解锁，happens-before于随后对这个锁的加锁。

volatile变量规则：对一个volatile域的写，happens-before于任意后续对这个volatile域的读。

传递性：如果A happens-before B，且B happens-before C，那么A happens-before C。

start()规则：如果线程A执行操作ThreadB.start()（启动线程B），那么A线程的ThreadB.start()操作happens-before于线程B中的任意操作。

join()规则：如果线程A执行操作ThreadB.join()并成功返回，那么线程B中的任意操作happens-before于线程A从ThreadB.join()操作成功返回。

程序中断规则：对线程interrupted()方法的调用先行于被中断线程的代码检测到中断时间的发生。

对象finalize规则：一个对象的初始化完成（构造函数执行结束）先行于发生它的finalize()方法的开始。

 

 

首先明确一点：假如有两个线程分别读写volatile变量时，线程A写入了某volatile变量，线程B在读取该volatile变量时，便能看到线程A对该volatile变量的写入操作，关键在这里，它不仅会看到对该volatile变量的写入操作，A线程在写volatile变量之前所有可见的共享变量，在B线程读同一个volatile变量后，都将立即变得对B线程可见。

 

 

 

/**

\* 发起20个线程，每个线程对race变量进行10000次自增操作，如果代码能够正确并发，

\* 则最终race的结果应为200000，但实际的运行结果却小于200000。

*

\* @author Colin Wang

*

*/

public class VolatileTest {

​    public static volatile int race = 0;

​    public static void increase() {

​        race++;

​    }

​    private static final int THREADS_COUNT = 20;

​    public static void main(String[] args) {

​        Thread[] threads = new Thread[THREADS_COUNT];

​        for (int i = 0; i < THREADS_COUNT; i++) {

​            threads[i] = new Thread(new Runnable() {

​                @Override

​                public void run() {

​                    for (int i = 0; i < 10000; i++) {

​                        increase();

​                    }

​                }

​            });

​            threads[i].start();

​        }

​         

​        while (Thread.activeCount() > 1)

​            Thread.yield();

​        System.out.println(race);

​    }

}

这便是因为race++操作不是一个原子操作，导致一些线程对变量race的修改丢失。

 

若要使用volatale变量，一般要符合以下两种场景：

变量的运算结果并不依赖于变量的当前值，或能够保证只有单一的线程修改变量的值。

变量不需要与其他的状态变量共同参与不变约束。

 

================================================================多重继承================================================================

在java中不充许继承两个或两个以上的类

像这样class c extends a ,b是不充许的

但可以用一种间接的方式实现：接口

 

Java是非常和善和理解我们的,它提供了两种方式让我们曲折来实现多重继承：接口和内部类。

 

在介绍内部类的时候谈到 内部类使得多继承的实现变得更加完美了，同时也明确了如果父类为抽象类或者具体类，那么我就仅能通过内部类来实现多重继承了。

 

 

================================================================异常================================================================

记住异常的性能代价高昂

 

需要记住的一件事是异常代价高昂，同时让代码运行缓慢。假如你有一个方法从 ResultSet 中进行读取，它经常会抛出 SQLException 而不是将 cursor 移到下一元素，这将会比不抛出异常的正常代码执行的慢的多。因此最大限度的减少不必要的异常捕捉，去修复真正的根本问题。不要仅仅是抛出和捕捉异常，如果你能使用 boolean 变量去表示执行结果，可能会得到更整洁、更高性能的解决方案。修正错误的根源，避免不必要的异常捕捉。

 

 

 

！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！

================================================================抽象类与接口================================================================

设计层次：

 

1、 抽象层次不同。抽象类是对类抽象，而接口是对行为的抽象。抽象类是对整个类整体进行抽象，包括属性、行为，但是接口却是对类局部（行为）进行抽象。

2、 跨域不同。抽象类所跨域的是具有相似特点的类，而接口却可以跨域不同的类。我们知道抽象类是从子类中发现公共部分，然后泛化成抽象类，子类继承该父类即可，但是接口不同。实现它的子类可以不存在任何关系，共同之处。

例如猫、狗可以抽象成一个动物类抽象类，具备叫的方法。鸟、飞机可以实现飞Fly接口，具备飞的行为，这里我们总不能将鸟、飞机共用一个父类吧！

所以说抽象类所体现的是一种继承关系，要想使得继承关系合理，父类和派生类之间必须存在”is-a” 关系，即父类和派生类在概念本质上应该是相同的。对于接口则不然，并不要求接口的实现者和接口定义在概念本质上是一致的， 仅仅是实现了接口定义的契约而已。

​    抽象类：共同的父类

​    接口： 实现同一个接口的类可以完全没关系

3、设计层次不同。对于抽象类而言，它是自下而上来设计的，我们要先知道子类才能抽象出父类，而接口则不同，它根本就不需要知道子类的存在，只需要定义一个规则即可，至于什么子类、什么时候怎么实现它一概不知。比如我们只有一个猫类在这里，如果你这是就抽象成一个动物类，是不是设计有点儿过度？我们起码要有两个动物类，猫、狗在这里，我们在抽象他们的共同点形成动物抽象类吧！所以说抽象类往往都是通过重构而来的！但是接口就不同，比如说飞，我们根本就不知道会有什么东西来实现这个飞接口，怎么实现也不得而知，我们要做的就是事前定义好飞的行为接口。所以说抽象类是自底向上抽象而来的，接口是自顶向下设计出来的。

 

 

 

================================================================商品搜索引擎—推荐系统设计================================================================

 

http://www.importnew.com/19834.html

 

 

================================================================BigDecimal进行精确运算================================================================

System.out.println(0.06+0.01);

 

0.06999999999999999

问题在哪里呢？原因在于我们的计算机是二进制的。浮点数没有办法是用二进制进行精确表示。

我们的CPU表示浮点数由两个部分组成：指数和尾数，这样的表示方法一般都会失去一定的精确度，有些浮点数运算也会产生一定的误差。

如：2.4的二进制表示并非就是精确的2.4。反而最为接近的二进制表示是 2.3999999999999999。浮点数的值实际上是由一个特定的数学公式计算得到的。

 

================================================================equals()================================================================

public boolean equals(Object obj) {

​    return (this == obj);

}

同时“==”比较两个对象的的内存地址

 

在java中进行比较，我们需要根据比较的类型来选择合适的比较方式：

1) 对象域，使用equals方法 。

2) 类型安全的枚举，使用equals或== 。

3) 可能为null的对象域 : 使用 == 和 equals 。

4) 数组域 : 使用 Arrays.equals 。

5) 除float和double外的原始数据类型 : 使用 == 。

6) float类型: 使用Float.foatToIntBits转换成int类型，然后使用==。

7) double类型: 使用Double.doubleToLongBit转换成long类型，然后使用==。

 

在equals()中使用getClass进行类型判断：

我们在覆写equals()方法时，一般都是推荐使用getClass来进行类型判断，不是使用instanceof。我们都清楚instanceof的作用是判断其左边对象是否为其右边类的实例，返回boolean类型的数据。可以用来判断继承中的子类的实例是否为父类的实现。注意后面这句话：可以用来判断继承中的子类的实例是否为父类的实现，正是这句话在作怪。（如果A，B都继承C呢？）

 

覆写equals时推荐使用getClass进行类型判断。而不是使用instanceof。

 

================================================================Dubbo================================================================

http://www.importnew.com/19732.html

 

远程服务调用的分布式框架

 

 

================================================================设计模式================================================================

http://www.importnew.com/19556.html

 

 

 

================================================================checked异常和unchecked异常================================================================

http://www.importnew.com/19489.html

 

这里之所以让大家清楚checked异常和unchecked异常概念，是因为：

Spring使用声明式事务处理，默认情况下，如果被注解的数据库操作方法中发生了unchecked异常，所有的数据库操作将rollback；如果发生的异常是checked异常，默认情况下数据库操作还是会提交的。

 

unchecked异常：

表示错误，程序的逻辑错误。是RuntimeException的子类，比如IllegalArgumentException, NullPointerException和IllegalStateException。

不需要在代码中显式地捕获unchecked异常做处理。

继承自java.lang.RuntimeException（而java.lang.RuntimeException继承自java.lang.Exception）。

 

checked异常：

表示无效，不是程序中可以预测的。比如无效的用户输入，文件不存在，网络或者数据库链接错误。这些都是外在的原因，都不是程序内部可以控制的。

必须在代码中显式地处理。比如try-catch块处理，或者给所在的方法加上throws说明，将异常抛到调用栈的上一层。

继承自java.lang.Exception（java.lang.RuntimeException除外）。

 

@Transactional的使用实例：

spring配置文件：

<bean id="appTransactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">

​      <property name="dataSource" ref="dataSource" />

</bean>

<tx:annotation-driven proxy-target-class="false" transaction-manager="appTransactionManager" />

 

使用@Transactional，在添加用户实现类方法加上注解

@Transactional(propagation=Propagation.REQUIRED)

public void addUser(User user) {

​    userDao.addUser(user);

​    String string  = null;

​    if(string.equals("")) {

​        int i = 0;

​    }

}

发现无法插入进去，但是如果把@Transactional去掉，即代码如下，虽然出现异常，但是数据库中还是有添加对应数据的：

 

 

一般使用是通过如下代码对方法或接口或类注释：

@Transactional(propagation=Propagation.NOT_SUPPORTED)

Propagation支持7种不同的传播机制：

REQUIRED：如果存在一个事务，则支持当前事务。如果没有事务则开启一个新的事务。

SUPPORTS： 如果存在一个事务，支持当前事务。如果没有事务，则非事务的执行。但是对于事务同步的事务管理器，PROPAGATION_SUPPORTS与不使用事务有少许不同。

NOT_SUPPORTED：总是非事务地执行，并挂起任何存在的事务。

REQUIRESNEW：总是开启一个新的事务。如果一个事务已经存在，则将这个存在的事务挂起。

MANDATORY：如果已经存在一个事务，支持当前事务。如果没有一个活动的事务，则抛出异常。

NEVER：总是非事务地执行，如果存在一个活动事务，则抛出异常

NESTED：如果一个活动的事务存在，则运行在一个嵌套的事务中。如果没有活动事务，则按REQUIRED属性执行。

 

下面是一些需要注意的事项，必须必须必须要看，不然遇到各种坑别说博主没有提醒你哦：

在需要事务管理的地方加@Transactional 注解。@Transactional 注解可以被应用于接口定义和接口方法、类定义和类的 public 方法上。

@Transactional 注解只能应用到 public 可见度的方法上。 如果你在 protected、private 或者 package-visible 的方法上使用 @Transactional 注解，它也不会报错， 但是这个被注解的方法将不会展示已配置的事务设置。

注意仅仅 @Transactional 注解的出现不足于开启事务行为，它仅仅 是一种元数据。必须在配置文件中使用配置元素，才真正开启了事务行为。

Spring团队建议在具体的类（或类的方法）上使用 @Transactional 注解，而不要使用在类所要实现的任何接口上。在接口上使用 @Transactional 注解，只能当你设置了基于接口的代理时它才生效。因为注解是 不能继承 的，这就意味着如果正在使用基于类的代理时，那么事务的设置将不能被基于类的代理所识别，而且对象也将不会被事务代理所包装。

@Transactional 的事务开启 ，或者是基于接口的 或者是基于类的代理被创建。所以在同一个类中一个方法调用另一个方法有事务的方法，事务是不会起作用的。

@Transactional 的事务开启 ，或者是基于接口的 或者是基于类的代理被创建。所以在同一个类中一个方法调用另一个方法有事务的方法，事务是不会起作用的。

这是因为同类方法的相互调用时它们的调用者总是当前对象this, 也就是说对于doA()方法, 同类的其他方法的调用使用doA()或者this.doA()是等义的. 这个调用是不经过代理对象的, 而@Transactional事务的处理是通过切面的方式添加进去的, 必须是代理对象的调用才能执行到切面附加的事务处理逻辑; 所以同类的不同方法的调用@Transactional 的事务是不会起作用的(除非自己手工处理). 这种情况也适用于所有通过代理进行处理的框架技术.典型的就是所有通过Annotation实现的框架.

 

 

 

================================================================java Files 类和 Paths 类的用法================================================================

Path就是取代File的

 

Path用于来表示文件路径和文件。可以有多种方法来构造一个Path对象来表示一个文件路径，或者一个文件：

 

1）首先是final类Paths的两个static方法，如何从一个路径字符串来构造Path对象：

​    Path path = Paths.get("C:/", "Xmp");

​    Path path2 = Paths.get("C:/Xmp");

​    

​    URI u = URI.create("[file:///C:/Xmp/dd");](file:///C:/Xmp/dd)        

​    Path p = Paths.get(u);

2）FileSystems构造：

​    Path path3 = FileSystems.getDefault().getPath("C:/", "access.log");

3）File和Path之间的转换，File和URI之间的转换：

​    File file = new File("C:/my.ini");

​    Path p1 = file.toPath();

​    p1.toFile();

​    file.toURI();

 

 

创建一个文件:

​    Path target2 = Paths.get("F:\\mystuff.txt");

​    try {

​        if (!Files.exists(target2))

​            Files.createFile(target2);

​    } catch (IOException e) {

​        e.printStackTrace();

​    }

​    

​    

​    Files.createDirectories(Paths.get("[C://TEST"));](file:///C:/TEST)

​    if(!Files.exists(Paths.get("[C://TEST](file:///C:/TEST)")))

​        Files.createFile(Paths.get("[C://TEST/test.txt"));](file:///C:/TEST/test.txt)

 

读取文件到String List中：

​    List<String> result2 = Files.readAllLines(Paths.get("F:\\mystuff.txt"), StandardCharsets.UTF_8);

​    结果：[HAA, OOO, QQQ, WWW, EEE, RRR, TTTY, YYY, 常志超, 隐隐于]

​    

写文件：

try {

​    BufferedWriter writer = Files.newBufferedWriter(Paths.get("C:\\my2.ini"), StandardCharsets.UTF_8);

​    writer.write("测试文件写操作");

​    writer.flush();

​    writer.close();

} catch (IOException e1) {

​    e1.printStackTrace();

}    

​    

遍历一个文件夹：

Path dir = Paths.get("D:\\webworkspace");

​    try(DirectoryStream<Path> stream = Files.newDirectoryStream(dir)){

​        for(Path e : stream){

​            System.out.println(e.getFileName());

​        }

​    }catch(IOException e){

}

 

 

上面是遍历单个目录，它不会遍历整个目录。遍历整个目录需要使用：Files.walkFileTree

public static void main(String[] args) throws IOException{

​        Path startingDir = Paths.get("C:\\apache-tomcat-8.0.21");

​        List<Path> result = new LinkedList<Path>();

​        Files.walkFileTree(startingDir, new FindJavaVisitor(result));

​        System.out.println("result.size()=" + result.size());        

​    }

​    

​    private static class FindJavaVisitor extends SimpleFileVisitor<Path>{

​        private List<Path> result;

​        public FindJavaVisitor(List<Path> result){

​            this.result = result;

​        }

​        @Override

​        public FileVisitResult visitFile(Path file, BasicFileAttributes attrs){

​            if(file.toString().endsWith(".java")){

​                result.add(file.getFileName());

​            }

​            return FileVisitResult.CONTINUE;

​        }

}

 

将目录下面所有符合条件的图片删除掉：filePath.matches(".*_[1|2]{1}\\.(?i)(jpg|jpeg|gif|bmp|png)"):

public static void main(String[] args) throws IOException {

​        Path startingDir = Paths.get("F:\\upload\\images");    // F:\\upload\\images\\2\\20141206

​        List<Path> result = new LinkedList<Path>();

​        Files.walkFileTree(startingDir, new FindJavaVisitor(result));

​        System.out.println("result.size()=" + result.size());

​        

​        System.out.println("done.");

​    }

​    

​    private static class FindJavaVisitor extends SimpleFileVisitor<Path>{

​        private List<Path> result;

​        public FindJavaVisitor(List<Path> result){

​            this.result = result;

​        }

​        

​        @Override

​        public FileVisitResult visitFile(Path file, BasicFileAttributes attrs){

​            String filePath = file.toFile().getAbsolutePath();       

​            if(filePath.matches(".*_[1|2]{1}\\.(?i)(jpg|jpeg|gif|bmp|png)")){

​                try {

​                    Files.deleteIfExists(file);

​                } catch (IOException e) {

​                    e.printStackTrace();

​                }

​              result.add(file.getFileName());

​            } return FileVisitResult.CONTINUE;

​        }

}

 

文件复制:

从文件复制到文件：Files.copy(Path source, Path target, CopyOption options);

从输入流复制到文件：Files.copy(InputStream in, Path target, CopyOption options);

从文件复制到输出流：Files.copy(Path source, OutputStream out);

 

​    

读取和设置文件权限：

Path profile = Paths.get("/home/digdeep/.profile");

PosixFileAttributes attrs = Files.readAttributes(profile, PosixFileAttributes.class);// 读取文件的权限

Set<PosixFilePermission> posixPermissions = attrs.permissions();

posixPermissions.clear();

String owner = attrs.owner().getName();

String perms = PosixFilePermissions.toString(posixPermissions);

System.out.format("%s %s%n", owner, perms);

 

posixPermissions.add(PosixFilePermission.OWNER_READ);

posixPermissions.add(PosixFilePermission.GROUP_READ);

posixPermissions.add(PosixFilePermission.OTHERS_READ);

posixPermissions.add(PosixFilePermission.OWNER_WRITE);

 

Files.setPosixFilePermissions(profile, posixPermissions);    // 设置文件的权限    

 

 

 

Files类简直强大的一塌糊涂，几乎所有文件和目录的相关属性，操作都有想要的api来支持。这里懒得再继续介绍了，详细参见 jdk8 的文档。

 

================================================================Files   JDK7 可以代替原来的 File类================================================================

 

public static Path createFile(Path path, FileAttribute<?>... attrs)

public static Path createDirectory(Path dir, FileAttribute<?>... attrs)

public static Path createDirectories(Path dir, FileAttribute<?>... attrs)

public static void delete(Path path) throws IOException {

public static Path copy(Path source, Path target, CopyOption... options)

public static Path move(Path source, Path target, CopyOption... options)

public static long size(Path path) throws IOException {     //返回字节数

 

public static InputStream newInputStream(Path path, OpenOption... options)

public static OutputStream newOutputStream(Path path, OpenOption... options)

public static BufferedReader newBufferedReader(Path path, Charset cs)

public static BufferedWriter newBufferedWriter(Path path, Charset cs,OpenOption... options)

 

public static byte[] readAllBytes(Path path) throws IOException {

public static List<String> readAllLines(Path path, Charset cs)

 

public static Path write(Path path, byte[] bytes, OpenOption... options)   //StandardOpenOption.APPEND

 

 

例子：

\*     OutputStream out = Files.newOutputStream(path);

*

\*     // append to an existing file, fail if the file does not exist

\*     out = Files.newOutputStream(path, APPEND);

*

\*     // append to an existing file, create file if it doesn't initially exist

\*     out = Files.newOutputStream(path, CREATE, APPEND);

*

\*     // always create new file, failing if it already exists

\*     out = Files.newOutputStream(path, CREATE_NEW);

 

 

DK7新特性，FileVisitor

 

================================================================ImageUtil================================================================

图片压缩：

https://www.aliyun.com/jiaocheng/1036.html

 

 

 

================================================================ 验证码 数据生成工具类================================================================

import java.awt.Color;

import java.awt.Font;

import java.awt.Graphics;

import java.awt.image.BufferedImage;

import java.io.FileOutputStream;

import java.io.IOException;

import java.io.OutputStream;

import java.util.Random;

import javax.imageio.ImageIO;

 

public class Main7 {

​    private static final char[] chars = { '0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'A', 'B', 'C', 'D', 'E',

​            'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z' };

​    // 字符数量

​    private static final int SIZE = 4;

​    // 干扰线数量

​    private static final int LINES = 5;

​    // 宽度

​    private static final int WIDTH = 80;

​    // 高度

​    private static final int HEIGHT = 40;

​    // 字体大小

​    private static final int FONT_SIZE = 30;

 

​    /**

​     \* 生成随机验证码及图片

​     */

​    public static Object[] createImage() {

​        StringBuffer sb = new StringBuffer();

​        // 1.创建空白图片

​        BufferedImage image = new BufferedImage(WIDTH, HEIGHT, BufferedImage.TYPE_INT_RGB);

​        // 2.获取图片画笔

​        Graphics graphic = image.getGraphics();

​        // 3.设置画笔颜色

​        graphic.setColor(Color.LIGHT_GRAY);

​        // 4.绘制矩形背景

​        graphic.fillRect(0, 0, WIDTH, HEIGHT);

​        // 5.画随机字符

​        Random ran = new Random();

​        for (int i = 0; i < SIZE; i++) {

​            // 取随机字符索引

​            int n = ran.nextInt(chars.length);

​            // 设置随机颜色

​            graphic.setColor(getRandomColor());

​            // 设置字体大小

​            graphic.setFont(new Font(null, Font.BOLD + Font.ITALIC, FONT_SIZE));

​            // 画字符

​            graphic.drawString(chars[n] + "", i * WIDTH / SIZE, HEIGHT / 2);

​            // 将字符保存，存入Session

​            sb.append(chars[n]);

​        }

​        // 6.画干扰线

​        for (int i = 0; i < LINES; i++) {

​            // 设置随机颜色

​            graphic.setColor(getRandomColor());

​            // 随机画线

​            graphic.drawLine(ran.nextInt(WIDTH), ran.nextInt(HEIGHT), ran.nextInt(WIDTH), ran.nextInt(HEIGHT));

​        }

​        // 7.返回验证码和图片

​        return new Object[] { sb.toString(), image };

​    }

 

​    /**

​     \* 随机取色

​     */

​    public static Color getRandomColor() {

​        Random ran = new Random();

​        Color color = new Color(ran.nextInt(256), ran.nextInt(256), ran.nextInt(256));

​        return color;

​    }

 

​    public static void main(String[] args) throws IOException {

​        Object[] objs = createImage();

​        BufferedImage image = (BufferedImage) objs[1];

​        OutputStream os = new FileOutputStream("f:/1.jpg");

​        ImageIO.write(image, "jpeg", os);

​        os.close();

​        

​        System.out.println(objs[0]);   //页面上的字符

​    }

 

}

 

 

================================================================在Java中如何高效的判断数组中是否包含某个元素================================================================

http://www.importnew.com/18700.html

 

public static boolean useLoop(String[] arr, String targetValue) {

​    for(String s: arr){

​        if(s.equals(targetValue))

​            return true;

​    }

​    return false;

}

 

 

 

================================================================40个Java多线程问题总结================================================================

http://www.importnew.com/18459.html

 

start()方法和run()方法的区别:

只有调用了start()方法，才会表现出多线程的特性，不同线程的run()方法里面的代码交替执行。如果只是调用run()方法，那么代码还是同步执行的，必须等待一个线程的run()方法里面的代码全部执行完毕之后，另外一个线程才可以执行其run()方法里面的代码。

也即：  run方法是相当于在主线程中执行了方法，并没有新开线程。

 

volatile的一个重要作用就是和CAS结合，保证了原子性，详细的可以参见java.util.concurrent.atomic包下的类，比如AtomicInteger。

 

 

CyclicBarrier和CountDownLatch的区别:

（1）CyclicBarrier的某个线程运行到某个点上之后，该线程即停止运行，直到所有的线程都到达了这个点，所有线程才重新运行；CountDownLatch则不是，某线程运行到某个点上之后，只是给某个数值-1而已，该线程继续运行

（2）CyclicBarrier只能唤起一个任务，CountDownLatch可以唤起多个任务

（3）CyclicBarrier可重用，CountDownLatch不可重用，计数值为0该CountDownLatch就不可再用了

 

 

一个线程如果出现了运行时异常会怎么样:

如果这个异常没有被捕获的话，这个线程就停止执行了。另外重要的一点是：如果这个线程持有某个某个对象的监视器，那么这个对象监视器会被立即释放

 

 

 

================================================================Java中如何获取到线程dump文件================================================================

死循环、死锁、阻塞、页面打开慢等问题，打线程dump是最好的解决问题的途径。所谓线程dump也就是线程堆栈，获取到线程堆栈有两步：

 

（1）获取到线程的pid，可以通过使用jps命令，在Linux环境下还可以使用ps -ef | grep java

 

（2）打印线程堆栈，可以通过使用jstack pid命令，在Linux环境下还可以使用kill -3 pid

 

另外提一点，Thread类提供了一个getStackTrace()方法也可以用于获取线程堆栈。这是一个实例方法，因此此方法是和具体线程实例绑定的，每次获取获取到的是具体某个线程当前运行的堆栈，

 

 

================================================================运行时异常和非运行时异常================================================================

异常的概念：

 

​                                                               |--->OutOfMemoryError

​                                 |---->VirtulMachineError------|

​            |------>Error--------|                             |--->StackOverFlowError

​            |                    |---->AWTError

​            |

Throwable---|

​            |

​            |                    |---->IOException------------------------>FileNotFoundException

​            |------>Exception----|

​                                 |---->RuntimeException（运行时异常）----->NullPointerException、ArithmeticException、ClassNotFoundException

 

​                                

Error（错误）:是程序无法处理的错误，表示运行应用程序中较严重问题。大多数错误与代码编写者执行的操作无关，而表示代码运行时 JVM（Java 虚拟机）出现的问题。例如，Java虚拟机运行错误（Virtual MachineError），当 JVM 不再有继续执行操作所需的内存资源时，将出现 OutOfMemoryError。这些异常发生时，Java虚拟机（JVM）一般会选择线程终止。

 

Exception（异常）：可以分为checked exceptions和unchecked exceptions

 

1，unchecked exceptions（运行时异常）都是RuntimeException类及其子类异常，就是我们在开发中测试功能时程序终止，控制台出现的异常，比如：

NullPointerException(空指针异常)、

IndexOutOfBoundsException(下标越界异常)

ClassCastException(类转换异常)

ArrayStoreException(数据存储异常，操作数组时类型不一致)

IO操作的BufferOverflowException异常

 

2， checked exceptions，非运行时异常 （编译异常）：是RuntimeException以外的异常，类型上都属于Exception类及其子类。从程序语法角度讲是必须进行处理的异常，如果不处理，程序就不能编译通过。如IOException、SQLException等以及用户自定义的Exception异常，一般情况下不自定义检查异常。

一个线程如果出现了运行时异常会怎么样：如果这个异常没有被捕获的话，这个线程就停止执行了。另外重要的一点是：如果这个线程持有某个某个对象的监视器，那么这个对象监视器会被立即释放（监视器可以先理解成锁）

 

生产者消费者模型的作用是什么：

（1）通过平衡生产者的生产能力和消费者的消费能力来提升整个系统的运行效率，这是生产者消费者模型最重要的作用

 

（2）解耦，这是生产者消费者模型附带的作用，解耦意味着生产者和消费者之间的联系少，联系越少越可以独自发展而不需要收到相互的制约

 

 

这是JDK强制的，wait()方法和notify()/notifyAll()方法在调用前都必须先获得对象的锁

 

 

================================================================wait()方法和notify()/notifyAll()方法在放弃对象监视器时有什么区别================================================================

wait()方法和notify()/notifyAll()方法在放弃对象监视器时有什么区别

wait()方法和notify()/notifyAll()方法在放弃对象监视器的时候的区别在于：wait()方法立即释放对象监视器，notify()/notifyAll()方法则会等待线程剩余代码执行完毕才会放弃对象监视器。

 

 

================================================================Linux环境下如何查找哪个线程使用CPU最长================================================================

这是一个比较偏实践的问题，这种问题我觉得挺有意义的。可以这么做：

 

（1）获取项目的pid，jps或者ps -ef | grep java，这个前面有讲过

 

（2）top -H -p pid，顺序不能改变

 

这样就可以打印出当前的项目，每条线程占用CPU时间的百分比。注意这里打出的是LWP，也就是操作系统原生线程的线程号，我笔记本山没有部署Linux环境下的Java工程，因此没有办法截图演示，网友朋友们如果公司是使用Linux环境部署项目的话，可以尝试一下。

 

使用”top -H -p pid”+”jps pid”可以很容易地找到某条占用CPU高的线程的线程堆栈，从而定位占用CPU高的原因，一般是因为不当的代码操作导致了死循环。

 

最后提一点，”top -H -p pid”打出来的LWP是十进制的，”jps pid”打出来的本地线程号是十六进制的，转换一下，就能定位到占用CPU高的线程的当前线程堆栈了。

 

 

================================================================Sleep(0)的妙用================================================================

Thread.Sleep(0)并非是真的要线程挂起0毫秒，意义在于这次调用Thread.Sleep(0)的当前线程确实的被冻结了一下，让其他线程有机会优先执行。

Thread.Sleep(0)是你的线程暂时放弃cpu，也就是释放一些未用的时间片给其他线程或进程使用，就相当于一个让位动作。

 

在线程没退出之前，线程有三个状态，就绪态，运行态，等待态。sleep(n)之所以在n秒内不会参与CPU竞争，是因为，当线程调用sleep(n)的时候，线程是由运行态转入等待态，线程被放入等待队列中，等待定时器n秒后的中断事件，当到达n秒计时后，线程才重新由等待态转入就绪态，被放入就绪队列中，等待队列中的线程是不参与cpu竞争的，只有就绪队列中的线程才会参与cpu竞争，所谓的cpu调度，就是根据一定的算法（优先级，FIFO等。。。），从就绪队列中选择一个线程来分配cpu时间。

 

而sleep(0)之所以马上回去参与cpu竞争，是因为调用sleep(0)后，因为0的原因，线程直接回到就绪队列，而非进入等待队列，只要进入就绪队列，那么它就参与cpu竞争。

 

 

 

================================================================自旋================================================================

很多synchronized里面的代码只是一些很简单的代码，执行时间非常快，此时等待的线程都加锁可能是一种不太值得的操作，因为线程阻塞涉及到用户态和内核态切换的问题。既然synchronized里面的代码执行得非常快，不妨让等待锁的线程不要被阻塞，而是在synchronized的边界做忙循环，这就是自旋。如果做了多次忙循环发现还没有获得锁，再阻塞，这样可能是一种更好的策略。

 

多线程中，对共享资源进行访问，为了防止并发引起的相关问题，通常都是引入锁的机制来处理并发问题。

获取到资源的线程A对这个资源加锁，其他线程比如B要访问这个资源首先要获得锁，而此时A持有这个资源的锁，只有等待线程A逻辑执行完，释放锁，这个时候B才能获取到资源的锁进而获取到该资源。

这个过程中，A一直持有着资源的锁，那么没有获取到锁的其他线程比如B怎么办？通常就会有两种方式：

\1. 一种是没有获得锁的进程就直接进入阻塞（BLOCKING），这种就是互斥锁

\2. 另外一种就是没有获得锁的进程，不进入阻塞，而是一直循环着，看是否能够等到A释放了资源的锁。

 

自旋锁（spin lock）是一种非阻塞锁，也就是说，如果某线程需要获取锁，但该锁已经被其他线程占用时，该线程不会被挂起，而是在不断的消耗CPU的时间，不停的试图获取锁。

互斥量（mutex）是阻塞锁，当某线程无法获取锁时，该线程会被直接挂起，该线程不再消耗CPU时间，当其他线程释放锁后，操作系统会激活那个被挂起的线程，让其投入运行。

 

自旋锁是计算机科学用于多线程同步的一种锁，线程反复检查锁变量是否可用。由于线程在这一过程中保持执行，因此是一种忙等待。

 

适用场景：

自旋锁避免了进程上下文的调度开销，因此对于线程只会阻塞很短时间的场合是有效的。

自旋锁比较适用于锁使用者保持锁时间比较短的情况，这种情况下自旋锁的效率要远高于互斥锁。

 

 

自旋锁可能潜在的问题

过多占用CPU的资源，如果锁持有者线程A一直长时间的持有锁处理自己的逻辑，那么这个线程B就会一直循环等待过度占用cpu资源

递归使用可能会造成死锁，不过这种场景一般写不出来

 

 

自旋锁可以使线程在没有取得锁的时候，不被挂起，而转去执行一个空循环，（即所谓的自旋，就是自己执行空循环），若在若干个空循环后，线程如果可以获得锁，则继续执行。若线程依然不能获得锁，才会被挂起。

使用自旋锁后，线程被挂起的几率相对减少，线程执行的连贯性相对加强。因此，对于那些锁竞争不是很激烈，锁占用时间很短的并发线程，具有一定的积极意义，但对于锁竞争激烈，单线程锁占用很长时间的并发程序，自旋锁在自旋等待后，往往毅然无法获得对应的锁，不仅仅白白浪费了CPU时间，最终还是免不了被挂起的操作 ，反而浪费了系统的资源。

 

在JDK1.6中，Java虚拟机提供-XX:+UseSpinning参数来开启自旋锁，使用-XX:PreBlockSpin参数来设置自旋锁等待的次数。

 

在JDK1.7开始，自旋锁的参数被取消，虚拟机不再支持由用户配置自旋锁，自旋锁总是会执行，自旋锁次数也由虚拟机自动调整。

 

 

 

================================================================怎样使用线程池================================================================

这是我在并发编程网上看到的一个问题，把这个问题放在最后一个，希望每个人都能看到并且思考一下，因为这个问题非常好、非常实际、非常专业。关于这个问题，个人看法是：

 

（1）高并发、任务执行时间短的业务，线程池线程数可以设置为CPU核数+1，减少线程上下文的切换

 

（2）并发不高、任务执行时间长的业务要区分开看：

 

a）假如是业务时间长集中在IO操作上，也就是IO密集型的任务，因为IO操作并不占用CPU，所以不要让所有的CPU闲下来，可以加大线程池中的线程数目，让CPU处理更多的业务

 

b）假如是业务时间长集中在计算操作上，也就是计算密集型任务，这个就没办法了，和（1）一样吧，线程池中的线程数设置得少一些，减少线程上下文的切换

 

（3）并发高、业务执行时间长，解决这种类型任务的关键不在于线程池而在于整体架构的设计，看看这些业务里面某些数据是否能做缓存是第一步，增加服务器是第二步，至于线程池的设置，设置参考（2）。最后，业务执行时间长的问题，也可能需要分析一下，看看能不能使用中间件对任务进行拆分和解耦。

 

线程的创建和销毁是非常耗 CPU 和内存的，因为这需要 JVM 和操作系统的参与。

 

 

JDK 中实现 ExecutorService 的类有：

ForkJoinPool

ThreadPoolExecutor

ScheduledThreadPoolExecutor

 

================================================================Java开发必会的Linux命令================================================================

http://www.importnew.com/17354.html

 

 

================================================================重写父类的方法一定要加@Override================================================================

重写父类的方法的时候，一定要在方法的上面加以@Override标志。这样一旦方法名称出错的时候，就可以有提示。

如果子类重写父类的方法，在子类方法前面加上@Override, 系统可以检查子类方法的参数是否与父类一致，在编译期尽早发现错误。

 

 

 

 

public SubClass() {}  

===>     

public SuperClass() {

​    setX(99);

}

===>    

@Override

public void setX(int x) {

​    super.setX(x);

​    mSubX = x;

​    System.out.println("SubX is assigned " + x);

}

===========>    

​        public void setX(int x) {

​            mSuperX = x;

​        }

 

 

 

 

public class SuperClass {

​    private int mSuperX;

​    

​    public SuperClass() {

​        setX(99);

​    }

​    public void setX(int x) {

​        mSuperX = x;

​    }

}

 

public class SubClass extends SuperClass {

​    private int mSubX = 1;

​    

​    public SubClass() {}

​    @Override

​    public void setX(int x) {

​        super.setX(x);

​        mSubX = x;

​        System.out.println("SubX is assigned " + x);   //此时mSubX确实是99

​    }

​    public void printX() {

​        System.out.println("SubX = " + mSubX);

​    }

​    

​    

​    public static void main(String[] args) {

​        SubClass sc = new SubClass();   

​        sc.printX();

​    }

}

 

结果：

SubX is assigned 99

SubX = 1

 

private int mSubX = 1;  ==> private int mSubX;

结果：

SubX is assigned 99

SubX = 99

 

所谓的默认初始化, 其实是我们要实例化一个对象之前, 需要一块内存放我们的数据, 这块内存被全部置为0, 这就是默认初始化了.

下面这两句话, 虽然效果一样, 但实际是有区别的.

private int mSubX;

private int mSubX = 0;

一般情况下, 这两句代码对程序没有任何影响(除非你遇到这个bug), 上面一句和下面一句的区别在于, 下面一句会导致<init>方法里面生成3条指令, 分别是aload_0, iconst_0, putfield #**, 而上面一句则不会.

所以如果你的成员变量使用默认值初始化, 就没必要自己赋那个默认值, 而且还能省3条指令.

 

 

真谛：

父类static成员 -> 子类static成员 -> 父类普通成员初始化和初始化块 -> 父类构造方法 -> 子类普通成员初始化和初始化块 -> 子类构造方法

 

 

我们都知道Java是面向对象的语言, 面向对象三大特性之一多态性. 假如父类构造方法中调用了某个方法, 这个方法恰好被子类重写了, 会发生什么?

根据多态性, 实际被调用的是子类的方法, 这个没错. 再考虑有继承时, 初始化的顺序. 如果是new一个子类, 那么初始化顺序是:

父类static成员 -> 子类static成员 -> 父类普通成员初始化和初始化块 -> 父类构造方法 -> 子类普通成员初始化和初始化块（{}） -> 子类构造方法

 

 

 

================================================================泛型中? super T和? extends T的区别================================================================

经常发现有List<? super T>、Set<? extends T>的声明，是什么意思呢？<? super T>表示包括T在内的任何T的父类，<? extends T>表示包括T在内的任何T的子类，下面我们详细分析一下两种通配符具体的区别。

 

 

 

================================================================终止一个线程？？================================================================

在 Java 中没有方式来终止一个线程，除非该线程自动退出。请务必牢记的这一原则，

while (true) {

  // Nothing

}

它做了什么？什么都没做，只是无止境的消耗 CPU。我们能终止它吗？在 Java 中是不行的。只有当你按下 Ctrl-C 来终止整个 JVM 时这段程序才会停止。在 Java 中没有方式来终止一个线程，除非该线程自动退出。请务必牢记的这一原则，其它东西就显而易见了。

 

 

 

 

================================================================数据结构  堆 ================================================================

树、堆、图等数据结构

 

堆:一棵完全二叉树，堆首先得符合完全二叉树的特点，否则不是堆。

数据结构中的堆跟平时我们讲的内存的堆还是有点区别的。数据结构中的堆其实是利用完全二叉树的结构来维护一组数据。

若设二叉树的深度为h，除第h层外，其它各层的结点数都达到最大个数，第h层所有的结点都连续集中在最左边，这就是完全二叉树。

 

堆的分类：

一般我们把堆分为大根堆与小根堆，也称最大堆，最小堆。顾名思义，就是堆的每个节点都大于它的子孙节点称为大根堆，堆的每个节点小于他的左右子孙节点称为小根堆。

 

从小到大排序，使用大顶堆；从大到小排序，使用小顶堆。

 

基本术语：

A：用于表示堆的数组，下标从1开始，一直到n

PARENT(t)：节点t的父节点，即floor(t/2)

LEFT(t)：节点t的左孩子节点，即:2*t

RIGHT(t)：节点t的右孩子节点，即:2*t+1

HEAP_SIZE(A)：堆A当前的元素数目

 

 

 

！！！！！！！！！！！！！！！！！！！！！！！！！！！！！

由于堆从逻辑上看是一颗完全二叉树，因此可以按照层序遍历的顺序将元素放入一维数组中。注意为了方便，数组的元素存放从索引 1 处开始（不是0）。采用数组来存放就很容易地找到某个结点 i 的双亲结点(i/2)，孩子结点(左孩子：2i，右孩子：2i+1)

！！！！！！！！！！！！！！！！！！！！！！！！！！！！！

 

 

https://www.cnblogs.com/hapjin/p/4622681.html

https://www.cnblogs.com/hapjin/p/4823702.html

http://www.360doc.com/content/17/0427/17/41726672_649135214.shtml

 

 

 

public interface MaxHeapInterface<T extends Comparable<? super T>> {

​    public void add(T newEntry);//向堆中添加元素

​    public T removeMax();//删除堆顶元素

​    public T getMax();//取得堆顶元素

​    public int getSize();//获得堆中元素个数

​    public void clear();//清空堆中元素

}

 

 

public class ArrayMaxHeap<T extends Comparable<? super T>> implements MaxHeapInterface<T>,java.io.Serializable {

 

 

​    private T[] heap;//用来存储堆元素的数组

​    private int lastIndex;//最后一个元素的索引

​    private static final int DEFAULT_INITIAL_CAPACITY = 25;

​    

​    public ArrayMaxHeap() {

​        this(DEFAULT_INITIAL_CAPACITY);

​    }

​    public ArrayMaxHeap(int initalCapacity){

​        heap = (T[]) new Comparable[initalCapacity];//???

​        lastIndex = 0;

​    }

​    

​    /*

​     \* @Task 根据给定的数组元素来构建最大堆

​     \* @param entries 将entries数组中的元素创建成堆

​     */

​    public ArrayMaxHeap(T[] entries){

​        heap = (T[]) new Comparable[entries.length + 1];

​        lastIndex = entries.length;

​        for(int index = 0; index < entries.length; index++)

​        {

​            heap[index + 1] = entries[index];//第0号位置不存放元素

​            System.out.println(heap[index + 1]);

​        }

//        System.out.println("lastIndex = " + lastIndex);

​        for(int index = lastIndex / 2; index >= 1; index--)

​            reheap(index);//从最后一个非叶结点到根结点调用reheap进行堆调整操作

//        for(int index = 1; index <= lastIndex; index++)

//            System.out.println(heap[index]);

​    }

​    

​    @Override

​    public void add(T newEntry) {

​        lastIndex++;

​        if(lastIndex >= heap.length)

​            doubleArray();//若堆空间不足，则堆大小加倍

​        int newIndex = lastIndex;//从最后一个元素开始逐渐向上与父结点比较

​        int parentIndex = newIndex / 2;

​        heap[0] = newEntry;//哨兵

​        while(newEntry.compareTo(heap[parentIndex]) > 0){

​            heap[newIndex] = heap[parentIndex];

​            newIndex = parentIndex;

​            parentIndex = newIndex / 2;

​        }

//        while(newIndex > 1 && (newEntry.compareTo(heap[parentIndex]) > 0)){

//            heap[newIndex] = heap[parentIndex];

//            newIndex = parentIndex;

//            parentIndex = newIndex / 2;

//        }

​        heap[newIndex] = newEntry;

​    }

​    private void doubleArray(){

​        T[] oldHeap = heap;

​        heap = (T[]) new Comparable[lastIndex * 2];

​        for(int i = 1; i < lastIndex; i++)//lastIndex 在未插入元素前先自增了 1

​            heap[i] = oldHeap[i];

​        oldHeap = null;//垃圾回收

​    }

 

​    @Override

​    public T removeMax() {

​        T root = null;

​        if(!isEmpty()){

​            root = heap[1];

​            heap[1] = heap[lastIndex];//将最后一个元素代替第一个元素

​            lastIndex--;//转化为删除最后一个元素

​            reheap(1);//在树根处进行堆调整

​        }

​        return root;

​    }

 

​    /*

​     \* @Task:将树根为rootIndex的半堆调整为新的堆，半堆：树的左右子树都是堆

​     \* @param rootIndex 以rootIndex为根的子树

​     */

​    private void reheap(int rootIndex){

​        boolean done = false;//标记堆调整是否完成

​        T orphan = heap[rootIndex];

​        int largeChildIndex = 2 * rootIndex;//默认左孩子的值较大

​        //堆调整基于以largeChildIndex为根的子树进行

​        while(!done && (largeChildIndex <= lastIndex)){

​            //largeChildIndex 标记rootIndex的左右孩子中较大的孩子

​            int leftChildIndex = largeChildIndex;//默认左孩子的值较大

​            int rightChildIndex = leftChildIndex + 1;

​            //右孩子也存在,比较左右孩子

​            if(rightChildIndex <= lastIndex && (heap[largeChildIndex].compareTo(heap[rightChildIndex] )< 0))

​                largeChildIndex = rightChildIndex;

​        //    System.out.println(heap[largeChildIndex]);//这里有问题。。使用构造函数创建时reheap。。。。。

​            if(orphan.compareTo(heap[largeChildIndex]) < 0){

​                heap[rootIndex] = heap[largeChildIndex];

​                rootIndex = largeChildIndex;

​                largeChildIndex = 2 * rootIndex;//总是默认左孩子的值较大

​            }

​            else//以rootIndex为根的子树已经构成堆了

​                done = true;

​        }

​        heap[rootIndex] = orphan;

​    }

​    

​    @Override

​    public T getMax() {

​        T root = null;

​        if(!isEmpty())

​            root = heap[1];

​        return root;

​    }

 

​    @Override

​    public int getSize() {

​        return lastIndex;

​    }

 

​    @Override

​    public void clear() {

​        for(;lastIndex > -1; lastIndex--)

​            heap[lastIndex] = null;

​        lastIndex = 0;

​    }

​    

​    public boolean isEmpty(){

​        return lastIndex < 1;//堆元素从数组下标为1处开始存放

​    }

}

 

 

public class HeapSort {

​    private static <T extends Comparable<? super T>> void reheap(T[] heap, int rootIndex, int lastIndex){

​        boolean done = false;//标记堆调整是否完成

​        T orphan = heap[rootIndex];

​        int largeChildIndex = 2 * rootIndex + 1;//默认左孩子的值较大

​        //堆调整基于以largeChildIndex为根的子树进行

​        while(!done && (largeChildIndex <= lastIndex)){

​            //largeChildIndex 标记rootIndex的左右孩子中较大的孩子

​            int leftChildIndex = largeChildIndex;//默认左孩子的值较大

​            int rightChildIndex = leftChildIndex + 1;

​            //右孩子也存在,比较左右孩子

​            if(rightChildIndex <= lastIndex && (heap[largeChildIndex].compareTo(heap[rightChildIndex] )< 0))

​                largeChildIndex = rightChildIndex;

​        //    System.out.println(heap[largeChildIndex]);//这里有问题。。使用构造函数创建时reheap。。。。。

​            if(orphan.compareTo(heap[largeChildIndex]) < 0){

​                heap[rootIndex] = heap[largeChildIndex];

​                rootIndex = largeChildIndex;

​                largeChildIndex = 2 * rootIndex + 1;//总是默认左孩子的值较大

​            }

​            else//以rootIndex为根的子树已经构成堆了

​                done = true;

​        }

​        heap[rootIndex] = orphan;

​    }

​    

​    public static <T extends Comparable<? super T>> void heapSort(T[] array, int n){

​        //直接在array上创建初始堆

​        for(int rootIndex = n/2 - 1; rootIndex >= 0; rootIndex--)

​            reheap(array, rootIndex, n-1);

​        swap(array, 0 , n-1);

​        //调整第i个元素(索引为i-1)与第n-i个元素交换后形成的半堆

​        for(int lastIndex = n-2; lastIndex > 0; lastIndex--){

​            reheap(array, 0 , lastIndex);

​            swap(array, 0, lastIndex);

​        }

​    }

​    

​    private static <T> void swap(T[] array, int from ,int to){

​        T temp = array[from];

​        array[from] = array[to];

​        array[to] = temp;

​    }

}

 

 

 

堆排序的应用场景：

 

https://blog.csdn.net/shakespeare001/article/details/51360732

虽然堆排序的时间复杂度与快速排序一样，但是实际开发中依然还是采用快速排序比较多，为什么呢

 

堆排序在访问数组中元素时，是跳着访问的，因此对CPU缓存没有快速排序友好。

同样的数据，堆排序的交换两个元素的次数比快速排序多。

 

 

堆可以直接看做一个优先队列，入队，即往堆中添加元素，并且按照优先级堆化，而出队时，即堆顶元素为优先级最高的元素。Java中的PriorityQueue是优先级队列的一种实现。

 

 

 

 

 

 

 

===================================================================================时间复杂度===================================================================================

对程序基本操作执行次数的统计

 

T（n） = 3n，执行次数是线性的。

for(int i=0; i<n; i++){;

​    System.out.println("等待一天");

​    System.out.println("等待一天");

​    System.out.println("吃一寸面包");

}

 

 

T（n） = 5logn，执行次数是对数的。

for(int i=1; i<n; i*=2){

   System.out.println("等待一天");

   System.out.println("等待一天");

   System.out.println("等待一天");

   System.out.println("等待一天");

   System.out.println("吃一半面包");

}

 

 

T（n） = 2，执行次数是常量的。

void eat3(int n){

   System.out.println("等待一天");

   System.out.println("吃一个鸡腿");

}

 

 

算法A的相对时间规模是T（n）= 100n，时间复杂度是O(n)

 

算法B的相对时间规模是T（n）= 5n^2，时间复杂度是O(n^2)

 

 

===================================================================================-1===================================================================================

 

某种意义上来说 -1 是 null 在int类型下的另一种形式。

 

// Bad

if (string.indexOf(character) != -1) { ... }

// Good

if (string.indexOf(character) >= 0) { ... }

 

 

 

你可以告诉我任何你想要的开闭原则，不过那都是胡说八道。我不相信你（可以正确继承我的类），也不相信我自己（不会意外地继承我的类）。因此除了接口（专门用于继承）都应该是严格的 final。可以查看我们的 Java 编码中 10 个微妙的最佳实践 中的#9。

// Bad

public void boom() { ... }

// Good. Don't touch.

public final void dontTouch() { ... }

是的，写成final。如果这样做对你来说没有意义，你也可以通过修改或重写字节码来改变类和方法，或者发送功能请求。我敢肯定重写类/方法并不是一个好主意。

 

 

===================================================================================反射机制===================================================================================

JAVA反射机制是在运行状态中，对于任意一个类，都能够知道这个类的所有属性和方法；对于任意一个对象，都能够调用它的任意一个方法；这种动态获取的以及动态调用对象的方法的功能称为Java的反射机制。

 

 

 

===================================================================================HTTPSession作为缓存===================================================================================

HTTPSession作为缓存: 用户不能多，因为Session是存储在服务器端的，一个用户一个session。

 

详细介绍Session缓存和Cache缓存的区别。

（1）最大的区别是Cache提供缓存依赖来更新数据，而Session只能依靠定义的缓存时间来判断缓存数据是否有效。

（2）即使应用程序终止，只要Cache.Add方法中定义的缓存时间未过期，下次开启应用程序时，缓存的数据依然存在。而Session缓存只是存在于一次会话中，会话结束后，数据也就失效了。

(会话是指一个终端用户与交互系统进行通讯的过程，比如从输入账户密码进入操作系统到退出操作系统就是一个会话过程。Session代表服务器与浏览器的一次会话过程，这个过程是连续的，也可以时断时续的。)

（3）Session容易丢失，导致数据的不确定性，而Cache不会出现这种情况。

（4）由于Session是每次会话就被加载，所以不适宜存放大量信息，否则会导致服务器的性能降低。而Cache则主要用来保存大容量信息，如数据库中的多个表。

（5）VS2005的测试版提供了将缓存保存在硬盘上的参数，但正式版中取消了这个功能，估计其在以后版本中会重新实现。而Session目前只能保存在内存中，对其性能有影响。

 

 

 

===================================================================================ThreadLocal===================================================================================

在Java中使用ThreadLocal变量是为了在一个特定的线程中绑定变量。这意味着每个线程都有它自己的单独实例。这种方法一般在一个线程中用于处理状态信息，例如用户授权。然而，一个ThreadLocal变量的生命周期与另外一个线程的生命周期是息息相关的。被遗忘的ThreadLocal变量很容易导致内存问题，尤其是在应用服务器中。

 

如果忘记了设置ThreadLocal变量，尤其是在应用服务器中，这很容易导致内存问题。应用服务器利用线程池避免常量不断创建和线程销毁。举个例子，一个HTTPServletRequest类在运行时得到一个空闲的已分配的线程，在执行完后将它回传到线程池中。如果应用程序逻辑使用ThreadLocal变量和忘记了显式地移除它们，这时，内存是不会被释放的。

 

根据线程池大小——在程序系统中这些线程池可以是几百个线程。同时，由ThreadLocal变量引用的对象的大小，这可能导致一些问题。例如，在最坏的情况下，一个200个线程的线程池和一个5M大小的线程池将会导致1 GB的不必要的内存占用。这将立即导致强烈的垃圾回收反应，同时导致糟糕的响应时间和潜在的OutOfMemoryError错误。

 

一个实际的例子就是在JBossWS 1.2.0版本中出现的一个bug（在JBossWS1.2.1版本已经被修复）——“DOMUtils doesn’t clear thread locals”。此问题就是ThreadLocal变量导致的，它引用了一个14MB的解析文档。

 

 

===================================================================================StringTokenizer===================================================================================

\1. StringTokenizer(String str) ：构造一个用来解析str的StringTokenizer对象。java默认的分隔符是“空格”、“制表符(‘\t’)”、“换行符(‘\n’)”、“回车符(‘\r’)”。

\2. StringTokenizer(String str, String delim) ：构造一个用来解析str的StringTokenizer对象，并提供一个指定的分隔符。

\3. StringTokenizer(String str, String delim, boolean returnDelims) ：构造一个用来解析str的StringTokenizer对象，并提供一个指定的分隔符，同时，指定是否返回分隔符。

 

String s = new String("This is a test string");

StringTokenizer st = new StringTokenizer(s);

System.out.println( "Token Total: " + st.countTokens() );

while( st.hasMoreElements() ){

​    System.out.println(st.nextToken());

}

 

String.Split（）使用正则表达式，而StringTokenizer的只是使用逐字分裂的字符。

如果不用正则表达式（StringTokenizer也不能使用正则表达式），StringTokenizer在截取字符串中的效率最高。

 

 

===================================================================================逻辑优化===================================================================================

使用局部变量

调用方法时传递的参数以及在调用中创建的临时变量都保存在栈 (Stack) 里面，读写速度较快。其他变量，如静态变量、实例变量等，都在堆 (heap) 中创建，读写速度较慢。清单 12 所示代码演示了使用局部变量和静态变量的操作时间对比

 

public class variableCompare {

​    public static int b = 0;

​         public static void main(String[] args){

​         int a = 0;

​         long starttime = System.currentTimeMillis();

​         for(int i=0;i<1000000;i++){

​            a++;//在函数体内定义局部变量    

​         }

​         System.out.println(System.currentTimeMillis() - starttime);

​        

​         starttime = System.currentTimeMillis();

​         for(int i=0;i<1000000;i++){

​            b++;//在函数体内定义局部变量

​         }

​         System.out.println(System.currentTimeMillis() - starttime);

​     }

}

 

运行结果：

0

15

 

位运算代替乘除法：

public class yunsuan {

​     public static void main(String args[]){

​         long start = System.currentTimeMillis();

​         long a=1000;

​         for(int i=0;i<10000000;i++){

​             a*=2;

​             a/=2;

​         }

​         System.out.println(a);

​         System.out.println(System.currentTimeMillis() - start);

​         start = System.currentTimeMillis();

​         for(int i=0;i<10000000;i++){

​             a<<=1;

​             a>>=1;

​         }

​         System.out.println(a);

​         System.out.println(System.currentTimeMillis() - start);

​     }

}

 

运行结果：

1000

546

1000

63

 

 

替换 switch：

关键字 switch 语句用于多条件判断，switch 语句的功能类似于 if-else 语句，两者的性能差不多。但是 switch 语句有性能提升空间。清单 16 所示代码演示了 Switch 与 if-else 之间的对比。

 

 

在循环体内，如果能够提取到循环体外的计算公式，最好提取出来，尽可能让程序少做重复的计算。

public class duplicatedCode {

​     public static void beforeTuning(){

​         long start = System.currentTimeMillis();

​         double a1 = Math.random();

​         double a2 = Math.random();

​         double a3 = Math.random();

​         double a4 = Math.random();

​         double b1,b2;

​         for(int i=0;i<10000000;i++){

​             b1 = a1*a2*a4/3*4*a3*a4;

​             b2 = a1*a2*a3/3*4*a3*a4;

​         }

​         System.out.println(System.currentTimeMillis() - start);

​     }

​     

​     public static void afterTuning(){

​         long start = System.currentTimeMillis();

​         double a1 = Math.random();

​         double a2 = Math.random();

​         double a3 = Math.random();

​         double a4 = Math.random();

​         double combine,b1,b2;

​         for(int i=0;i<10000000;i++){

​             combine = a1*a2/3*4*a3*a4;

​             b1 = combine*a4;

​             b2 = combine*a3;

​         }

​         System.out.println(System.currentTimeMillis() - start);

​     }

​     

​     public static void main(String[] args){

​         duplicatedCode.beforeTuning();

​         duplicatedCode.afterTuning();

​     }

}

 

运行结果：

202

110

 

 

优化循环：

public class reduceLoop {

​    public static void beforeTuning(){

​         long start = System.currentTimeMillis();

​         int[] array = new int[9999999];

​         for(int i=0;i<9999999;i++){

​             array[i] = i;

​         }

​         System.out.println(System.currentTimeMillis() - start);

​    }

​     

​    public static void afterTuning(){

​         long start = System.currentTimeMillis();

​         int[] array = new int[9999999];

​         for(int i=0;i<9999999;i+=3){

​             array[i] = i;

​             array[i+1] = i+1;

​             array[i+2] = i+2;

​         }

​         System.out.println(System.currentTimeMillis() - start);

​    }

​     

​    public static void main(String[] args){

​        reduceLoop.beforeTuning();

​        reduceLoop.afterTuning();

​    }

}

 

运行结果：

265

31

 

 

===================================================================================System.arraycopy===================================================================================

public static native void arraycopy(Object src, int srcPos, Object dest, int destPos, int length);

src – 源数组；srcPos – 源数组中的起始位置； dest – 目标数组；destPos – 目标数据中的起始位置；length – 要复制的数组元素的数量。

 

===================================================================================hashCode()===================================================================================

 

 

===================================================================================Java集合===================================================================================

ArrayList

以数组实现。节约空间，但数组有容量限制。超出限制时会增加50%容量，用System.arraycopy()复制到新的数组，因此最好能给出数组大小的预估值。默认第一次插入元素时创建大小为10的数组。

按数组下标访问元素–get(i)/set(i,e) 的性能很高，这是数组的基本优势。

直接在数组末尾加入元素–add(e)的性能也高，但如果按下标插入、删除元素–add(i,e), remove(i), remove(e)，则要用System.arraycopy()来移动部分受影响的元素，性能就变差了，这是基本劣势。

 

LinkedList

以双向链表实现。链表无容量限制，但双向链表本身使用了更多空间，也需要额外的链表指针操作。

按下标访问元素–get(i)/set(i,e) 要悲剧的遍历链表将指针移动到位(如果i>数组大小的一半，会从末尾移起)。

插入、删除元素时修改前后节点的指针即可，但还是要遍历部分链表的指针才能移动到下标所指的位置，只有在链表两头的操作–add(), addFirst(),removeLast()或用iterator()上的remove()能省掉指针的移动。

 

CopyOnWriteArrayList

并发优化的ArrayList。用CopyOnWrite策略，在修改时先复制一个快照来修改，改完再让内部指针指向新数组。

因为对快照的修改对读操作来说不可见，所以只有写锁没有读锁，加上复制的昂贵成本，典型的适合读多写少的场景。如果更新频率较高，或数组较大时，还是Collections.synchronizedList(list)，对所有操作用同一把锁来保证线程安全更好。

增加了addIfAbsent(e)方法，会遍历数组来检查元素是否已存在，性能可想像的不会太好。

 

 

===================================================================================DelayQueue===================================================================================

虽然我们不能让公司的消息队列延迟发送，但是我们可以延迟处理。当收到消息时先不处理，放入延迟消息队列中，另外一个线程再从延迟队列中获得数据进行处理。

DelayQueue是一个支持延时获取元素的无界阻塞队列。队列使用PriorityQueue来实现。队列中的元素必须实现Delayed接口，在创建元素时可以指定多久才能从队列中获取当前元素。只有在延迟期满时才能从队列中提取元素。

 

DelayQueue非常有用，可以运用在以下两个应用场景：

缓存系统的设计：使用DelayQueue保存缓存元素的有效期，使用一个线程循环查询DelayQueue，一旦能从DelayQueue中获取元素时，就表示有缓存到期了。 

定时任务调度：使用DelayQueue保存当天要执行的任务和执行时间，一旦从DelayQueue中获取到任务就开始执行，比如Timer就是使用DelayQueue实现的。

 

public class DelayQueue<E extends Delayed> extends AbstractQueue<E> implements BlockingQueue<E>

 

放入DelayQueue的对象需要实现Delayed接口。

 

Delayed接口的定义很简单：只有一个getDelay(TimeUnit)方法，该方法返回与此对象相关的的剩余时间。同时我们看到Delayed接口继承自Comperable接口，所以实现Delayed接口的类还必须要定义一个compareTo方法，该方法提供与此接口的getDelay方法一致的排序。

 

public interface Delayed extends Comparable<Delayed> {

​    /**

​     \* Returns the remaining delay associated with this object, in the

​     \* given time unit.

​     *

​     \* @param unit the time unit

​     \* @return the remaining delay; zero or negative values indicate

​     \* that the delay has already elapsed

​     */

​    long getDelay(TimeUnit unit);

}

 

 

DelayQueue 是 Delayed 元素的一个无界阻塞队列，只有在延迟期满时才能从中提取元素。该队列的头部 是延迟期满后保存时间最长的 Delayed 元素。如果延迟都还没有期满，则队列没有头部，并且 poll 将返回 null。当一个元素的 getDelay(TimeUnit.NANOSECONDS) 方法返回一个小于等于 0 的值时，将发生到期。即使无法使用 take 或 poll 移除未到期的元素，也不会将这些元素作为正常元素对待。例如，size 方法同时返回到期和未到期元素的计数。此队列不允许使用 null 元素。

 

DelayQueue中比较重要的字段如下：

private final transient ReentrantLock lock = new ReentrantLock();

private final PriorityQueue<E> q = new PriorityQueue<E>();

private Thread leader = null;

private final Condition available = lock.newCondition();

 

DelayQueue的大致实现思路了：

以支持优先级的PriorityQueue无界队列作为一个容器，因为元素都必须实现Delayed接口，可以根据元素的过期时间来对元素进行排列，因此，先过期的元素会在队首，每次从队列里取出来都是最先要过期的元素。

 

 

 

 

 

 

 

 

public class Main9 {

​    public static void main(String[] args) {

​        DelayQueue<DelayedElement> delayQueue = new DelayQueue<DelayedElement>();

 

​        // 生产者

​        producer(delayQueue);

 

​        // 消费者

​        consumer(delayQueue);

 

​        while (true) {

​            try {

​                TimeUnit.HOURS.sleep(1);

​            } catch (InterruptedException e) {

​                e.printStackTrace();

​            }

​        }

​    }

 

​    /**

​     \* 每100毫秒创建一个对象，放入延迟队列，延迟时间1毫秒

​     *

​     \* @param delayQueue

​     */

​    private static void producer(final DelayQueue<DelayedElement> delayQueue) {

​        new Thread(new Runnable() {

​            @Override

​            public void run() {

​                int i = 10;

​                while (i > 0) {

​                    try {

​                        TimeUnit.MILLISECONDS.sleep(100);

​                    } catch (InterruptedException e) {

​                        e.printStackTrace();

​                    }

 

​                    DelayedElement element = new DelayedElement(5000, "test");

​                    delayQueue.offer(element);

​                    System.out.println(System.currentTimeMillis() + "--- offered : " + element);

​                    i--;

​                }

​            }

​        }).start();

 

​    }

 

​    /**

​     \* 消费者，从延迟队列中获得数据,进行处理

​     *

​     \* @param delayQueue

​     */

​    private static void consumer(final DelayQueue<DelayedElement> delayQueue) {

​        new Thread(new Runnable() {

​            @Override

​            public void run() {

​                while (true) {

​                    DelayedElement element = null;

​                    try {

​                        element = delayQueue.take();

​                    } catch (InterruptedException e) {

​                        e.printStackTrace();

​                    }

​                    System.out.println(System.currentTimeMillis() + "---" + element);

​                }

​            }

​        }).start();

​    }

}

 

public class DelayedElement implements Delayed{

​    private final long delay; //延迟时间

​    private final long expire;  //到期时间

​    private final String msg;   //数据

​    private final long now; //创建时间

 

​    public DelayedElement(long delay, String msg) {

​        this.delay = delay;

​        this.msg = msg;

​        expire = System.currentTimeMillis() + delay;    //到期时间 = 当前时间+延迟时间

​        now = System.currentTimeMillis();

​    }

 

​    /**

​     \* 需要实现的接口，获得延迟时间   用过期时间-当前时间

​     \* @param unit

​     \* @return

​     */

​    @Override

​    public long getDelay(TimeUnit unit) {

​        return unit.convert(this.expire - System.currentTimeMillis() , TimeUnit.MILLISECONDS);

​    }

 

​    /**

​     \* 用于延迟队列内部比较排序   当前时间的延迟时间 - 比较对象的延迟时间

​     \* @param o

​     \* @return

​     */

​    @Override

​    public int compareTo(Delayed o) {

​        return (int) (this.getDelay(TimeUnit.MILLISECONDS) -o.getDelay(TimeUnit.MILLISECONDS));

​    }

 

​    @Override

​    public String toString() {

​        final StringBuilder sb = new StringBuilder("DelayedElement{");

​        sb.append("delay=").append(delay);

​        sb.append(", expire=").append(expire);

​        sb.append(", msg='").append(msg).append('\'');

​        sb.append(", now=").append(now);

​        sb.append('}');

​        return sb.toString();

​    }

}

 

===================================================================================Java 序列化===================================================================================

一种将 Java 对象的状态转换为字节数组，以便存储或传输的机制，以后，仍可以将字节数组转换回 Java 对象原有的状态。

 

实际上，序列化的思想是 “冻结” 对象状态，传输对象状态（写到磁盘、通过网络传输等等），然后 “解冻” 状态，重新获得可用的 Java 对象。所有这些事情的发生有点像是魔术，这要归功于 ObjectInputStream/ObjectOutputStream 类、完全保真的元数据以及程序员愿意用Serializable 标识接口标记他们的类，从而 “参与” 这个过程。

 

 

public class Person implements java.io.Serializable{

​    private String firstName;

​    private String lastName;

​    private int age;

​    private Person spouse;

}

 

 

public class PersonTest {

​    public static void main(String[] args) {

​        try

​        {

​            new File("tempdata.ser").delete();    

​            Person ted = new Person("Ted", "Neward", 39);

​            Person charl = new Person("Charlotte",

​                "Neward", 38);

​            ted.setSpouse(charl); charl.setSpouse(ted);

​            FileOutputStream fos = new FileOutputStream("tempdata.ser");

​            ObjectOutputStream oos = new ObjectOutputStream(fos);

​            oos.writeObject(ted);

​            oos.writeObject(charl);

​            oos.close();

​            

​            FileInputStream fis = new FileInputStream("tempdata.ser");

​            ObjectInputStream ois = new ObjectInputStream(fis);

​            Person ted2 = (Person) ois.readObject();

​            System.out.println(ted2.toString());

​            Person ted3 = (Person) ois.readObject();

​            System.out.println(ted3.toString());

​            ois.close();

​            new File("tempdata.ser").delete();

​        }

​        catch (Exception ex)

​        {

​            System.out.println(ex.getMessage());

​        }

​    }

}

 

结果：

[Person: firstName=Ted lastName=Neward age=39 spouse=Charlotte]

[Person: firstName=Charlotte lastName=Neward age=38 spouse=Ted]

 

 

 

===================================================================================java  Deque===================================================================================

Deque则是双向队列,它支持从两个端点方向检索和插入元素

public interface Deque<E> extends Queue<E> {

 

ArrayDeque和LinkedList：

从效率来看,ArrayDeque要比LinkedList在两端增删元素上更为高效,因为没有在节点创建删除上的开销.最适合使用LinkedList的情况是迭代队列时删除当前迭代的元素

此外LinkedList可能是在遍历元素时最差的数据结构,并且也LinkedList占用更多的内存,因为LinkedList是通过链表连接其整个队列,它的元素在内存中是随机分布的,需要通过每个节点包含的前后节点的内存地址去访问前后元素.

总体ArrayDeque要比LinkedList更优越,在大队列的测试上有3倍与LinkedList的性能,最好的是给ArrayDeque一个较大的初始化大小,以避免底层数组扩容时数据拷贝的开销.

LinkedBlockingDeque是Deque的并发实现,在队列为空的时候,它的takeFirst,takeLast会阻塞等待队列处于可用状态

 

public static void main(String[] args) {       

​        Deque<String> deque = new LinkedList<String>();

​        deque.add("d");

​        deque.add("e");

​        deque.add("f");

​        

​        //从队首取出元素，不会删除

​        System.out.println("队首取出元素:"+deque.peek());

​        System.out.println("队列为:"+deque);

​        

​        //从队首加入元素(队列有容量限制时用，无则用addFirst)

​        deque.offerFirst("c");

​        System.out.println("队首加入元素后为："+deque);

​        //从队尾加入元素(队列有容量限制时用，无则用addLast)

​        deque.offerLast("g");

​        System.out.println("队尾加入元素后为："+deque);

​        

​        //队尾加入元素

​        deque.offer("h");

​        System.out.println("队尾加入元素后为："+deque);

​        

​        //获取并移除队列第一个元素,pollFirst()也是，区别在于队列为空时,removeFirst会抛出NoSuchElementException异常，后者返回null

​        deque.removeFirst();

​        System.out.println("获取并移除队列第一个元素后为:"+deque);

​        

​        //获取并移除队列第一个元素,此方法与pollLast 唯一区别在于队列为空时,removeLast会抛出NoSuchElementException异常，后者返回null

​        deque.removeLast();

​        System.out.println("获取并移除队列最后一个元素后为:"+deque);

​        

​        //获取队列第一个元素.此方法与 peekFirst 唯一的不同在于：如果此双端队列为空，它将抛出NoSuchElementException，后者返回null

​        System.out.println("获取队列第一个元素为:"+deque.getFirst());

​        System.out.println("获取队列第一个元素后为:"+deque);

​        

​        //获取队列最后一个元素.此方法与 peekLast 唯一的不同在于：如果此双端队列为空，它将抛出NoSuchElementException，后者返回null

​        System.out.println("获取队列最后一个元素为:"+deque.getLast());

​        System.out.println("获取队列第一个元素后为:"+deque);

​        

​        //循环获取元素并在队列移除元素

​        while(deque.size()>0){

​            System.out.println("获取元素为："+ deque.pop()+" 并删除");

​        }

​        System.out.println("队列为:"+deque);

}

 

队首取出元素:d

队列为:[d, e, f]

队首加入元素后为：[c, d, e, f]

队尾加入元素后为：[c, d, e, f, g]

队尾加入元素后为：[c, d, e, f, g, h]

获取并移除队列第一个元素后为:[d, e, f, g, h]

获取并移除队列最后一个元素后为:[d, e, f, g]

获取队列第一个元素为:d

获取队列第一个元素后为:[d, e, f, g]

获取队列最后一个元素为:g

获取队列第一个元素后为:[d, e, f, g]

获取元素为：d 并删除

获取元素为：e 并删除

获取元素为：f 并删除

获取元素为：g 并删除

队列为:[]

 

1.使用队列的时候，new LinkedList的时候为什么用deque接收，不用LinkedList呢？

　　答：deque继承queue接口，因为它有两个实现，LinkedList与ArrayDeque。用deque接收是因为向上转型(子类往父类转，会丢失子类的特殊功能)了。可以试试，用get()方法，LinkedList接收才有。

2.为什么有一个实现还不够，还弄两个呢，它们总有区别吧？

　　答：ArrayDeque是基于头尾指针来实现的Deque，意味着不能访问除第一个和最后一个元素。想访问得用迭代器，可以正反迭代。

　　　　ArrayDeque一般优于链表队列/双端队列，有限数量的垃圾产生（旧数组将被丢弃在扩展），建议使用deque，ArrayDeque优先。

 

 

当 Deque 当做 队列使用时（FIFO），添加元素是添加到队尾，删除时删除的是头部元素.

Deque 也能当栈用（后进先出）。这时入栈、出栈元素都是在 双端队列的头部 进行。

 

 

Deque 与 工作密取:

什么是工作密取呢？

在 生产者-消费者 模式中，所有消费者都从一个工作队列中取元素，一般使用阻塞队列实现；

而在 工作密取 模式中，每个消费者有其单独的工作队列，如果它完成了自己双端队列中的全部工作，那么它就可以从其他消费者的双端队列末尾秘密地获取工作。

工作密取 模式 对比传统的 生产者-消费者 模式，更为灵活，因为多个线程不会因为在同一个工作队列中抢占内容发生竞争。在大多数时候，它们只是访问自己的双端队列。即使需要访问另一个队列时，也是从 队列的尾部获取工作，降低了队列上的竞争程度。

 

 

===================================================================================Collections.unmodifiableCollection===================================================================================

当一个集合被作为参数传递给一个函数时，如何才可以确保函数不能修改它？

 

在作为参数传递之前，我们可以使用Collections.unmodifiableCollection(Collection c)方法创建一个只读集合，这将确保改变集合的任何操作都会抛出UnsupportedOperationException。

 

 

 

===================================================================================java 23种 设计模式 深入理解===================================================================================

 

 

 

 

 

===================================================================================Java反转字符串===================================================================================

StringBuilder java.lang.StringBuilder.reverse()

 

使用堆栈:

public class ReverseStringUsingStack {

​    public static String reverse(String str) {

​        if (str == null || str.equals(""))

​            return str;

​        Stack < Character > stack = new Stack < Character > ();

​        char[] ch = str.toCharArray();

​        for (int i = 0; i < str.length(); i++)

​            stack.push(ch[i]);

​        int k = 0;

​        while (!stack.isEmpty()) {

​            ch[k++] = stack.pop();

​        }

​        return String.copyValueOf(ch);

​    }

​    public static void main(String[] args) {

​        String str = "javaguides";

​        str = reverse(str); // string is immutable

​        System.out.println("Reverse of the given string is : " + str);

​    }

}

 

 

 

 

===================================================================================判空===================================================================================

public static boolean isNullOrEmpty(Object o) {

​    return o == null || String.valueOf(o).trim().length() == 0;

}

 

=================================================================================== AntPathMatcher 类 URLs 字符串匹配===================================================================================

可以做URLs匹配，规则如下：

？匹配一个字符

*匹配0个或多个字符

**匹配0个或多个目录

 

用例如下：

/trip/api/*x    匹配 /trip/api/x，/trip/api/ax，/trip/api/abx ；但不匹配 /trip/abc/x；

/trip/a/a?x    匹配 /trip/a/abx；但不匹配 /trip/a/ax，/trip/a/abcx

/**/api/alie    匹配 /trip/api/alie，/trip/dax/api/alie；但不匹配 /trip/a/api

/**/*.htmlm   匹配所有以.htmlm结尾的路径

 

 

private String[] whiteListURLs = null;

private final PathMatcher pathMatcher = new AntPathMatcher();

 

private boolean isWhiteURL(String currentURL) {

​    for (String whiteURL : whiteListURLs) {

​        if (pathMatcher.match(whiteURL, currentURL)) {

​            //logger.debug("url filter : white url list matches : [{}] match [{}] continue", whiteURL, currentURL);

​            return true;

​        }

​        //logger.debug("url filter : white url list not matches : [{}] match [{}]", whiteURL, currentURL);

​    }

​    return false;

}

 

 

=================================================================================== DatabaseMetaData===================================================================================

DatabaseMetaData类是java.sql包中的类，利用它可以获取我们连接到的数据库的结构、存储等很多信息

​    (1) DatabaseMetaData实例的获取

​        Connection conn = DriverManager.getConnection(……)；

​        DatabaseMetaData dbmd = Conn.getMetaData();

​        创建了这个实例，就可以使用它的方法来获取数据库得信息。主要使用如下的方法：

 

   (2) 获得当前数据库以及驱动的信息

​        dbmd.getDatabaseProductName()：用以获得当前数据库是什么数据库。比如oracle，access等。返回的是字符串。

​        dbmd.getDatabaseProductVersion()：获得数据库的版本。返回的字符串。

​        dbmd.getDriverVersion()：获得驱动程序的版本。返回字符串。

​        dbmd.getTypeInfo() ：获得当前数据库的类型信息

 

 

private static String getDatabaseProductName(DataSource dataSource) throws SQLException {

​    Connection con = null;

​    try {

​        con = dataSource.getConnection();

​        DatabaseMetaData metaData = con.getMetaData();

​        return metaData.getDatabaseProductName();

​    } finally {

​        if (con != null) {

​            try {

​                con.close();

​            } catch (SQLException e) {

​               logger.error("连接关闭失败{}",e);

​            }

​        }

​    }

}

 

=================================================================================== Java Number ===================================================================================

一般情况下我们会使用数据的基本数据类型：byte、int、short、long、double、float、boolean、char；

对应的包装类型也有八种：Byte、Integer、Short、Long、Double、Float、Character、Boolean;

包装类型都是用final声明了，不可以被继承重写；

 

public abstract class Number implements java.io.Serializable {

 

​    public abstract int intValue();

 

​    public abstract long longValue();

 

​    public abstract float floatValue();

 

​    public abstract double doubleValue();

 

​    public byte byteValue() {

​        return (byte)intValue();

​    }

 

​    public short shortValue() {

​        return (short)intValue();

​    }

 

​    private static final long serialVersionUID = -8742448824652078965L;

}

 

 

 

 

=================================================================================== NumberFormat DecimalFormat ===================================================================================

NumberFormat nf=NumberFormat.getInstance();

System.out.println("格式化后显示数字："+nf.format(10000000));

System.out.println("格式化后显示数字："+nf.format(10000.345));

 

格式化后显示数字：10,000,000

格式化后显示数字：10,000.345

 

DecimalFormat也是Format的一个子类，主要的作用是用来格式化数字，当然，在格式化数字的时候要比直接使用NumberFormat更加方便，因为可以直接指定按用户自定义的方式进行格式化操作，与SimpleDateFormat类似，如果要想进行自定义格式化操作，则必须指定格式化操作的模板。

 

 

 

public void format(String pattern, double value) {

​    DecimalFormat df = new DecimalFormat(pattern);

​    String str = df.format(value);

​    System.out.println("使用" + pattern + "\t格式化数字" + value + "：\t" + str);

}

 

public static void main(String[] args) {

​    Main12 demo = new Main12();

​    demo.format("###,###.###", 111222.34567);

​    demo.format("000,000.000", 11222.34567);

​    demo.format("###,###.###$", 111222.34567);

​    demo.format("000,000.000￥", 11222.34567);

​    demo.format("##.###%", 0.345678); // 使用百分数形式

​    demo.format("00.###%", 0.0345678); // 使用百分数形式

​    demo.format("###.###\u2030", 0.345678); // 使用千分数形式

 

}

 

使用###,###.###    格式化数字111222.34567：    111,222.346

使用000,000.000    格式化数字11222.34567：    011,222.346

使用###,###.###$    格式化数字111222.34567：    111,222.346$

使用000,000.000￥    格式化数字11222.34567：    011,222.346￥

使用##.###%    格式化数字0.345678：    34.568%

使用00.###%    格式化数字0.0345678：    03.457%

使用###.###‰    格式化数字0.345678：    345.678‰

 

 

===================================================================================  进制转换 ===================================================================================

public class HexUtil {

​    final static char[] digits = {

​              '0', '1', '2', '3', '4', '5', '6', '7',

​              '8','9', 'A', 'B', 'C', 'D', 'E', 'F',

​              'G', 'H','J', 'K', 'L','M', 'N',  'P',

​              'R', 'S', 'T', 'U', 'W', 'X', 'Y','Z',

​              'a', 'b', 'c', 'd', 'e', 'f',

​              'g', 'h','j', 'k', 'l','m', 'n',  'p',

​              'r', 's', 't', 'u', 'w', 'x', 'y','z'

​              

​         };

 

​    /**

​     \* 将十进制的数字转换为指定进制的字符串。

​     *

​     \* @param i

​     \*            十进制的数字。

​     \* @param system

​     \*            指定的进制，常见的2/8/16。

​     \* @return 转换后的字符串。

​     */

​    public static String numericToString(long i, int system) {

​        long num = 0;

​        if (i < 0) {

​            num = ((long) 2 * 0x7fffffff) + i + 2;

​        } else {

​            num = i;

​        }

​        char[] buf = new char[32];

​        int charPos = 32;

​        while ((num / system) > 0) {

​            buf[--charPos] = digits[(int) (num % system)];

​            num /= system;

​        }

​        buf[--charPos] = digits[(int) (num % system)];

​        return new String(buf, charPos, (32 - charPos));

​    }

 

​    /**

​     \* 将其它进制的数字（字符串形式）转换为十进制的数字。

​     *

​     \* @param s

​     \*            其它进制的数字（字符串形式）

​     \* @param system

​     \*            指定的进制，常见的2/8/16。

​     \* @return 转换后的数字。

​     */

​    public static int stringToNumeric(String s, int system) {

​        char[] buf = new char[s.length()];

​        s.getChars(0, s.length(), buf, 0);

​        long num = 0;

​        for (int i = 0; i < buf.length; i++) {

​            for (int j = 0; j < digits.length; j++) {

​                if (digits[j] == buf[i]) {

​                    num += j * Math.pow(system, buf.length - i - 1);

​                    break;

​                }

​            }

​        }

​        return (int) num;

​    }

}

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 

 