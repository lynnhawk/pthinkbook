# 第五节 业务组件：Bu

业务组件需要继承com.pthink.cloudapp.standard.abstracts.Atom，就可以被框架自动加载和管理。每个类按照框架要求将输入输出的信息编写相应的注解后就可以自动发布到服务器的http端口供使用者查看。

---

范例如下：

```java
package com.pthink.cloudapp.examples;


import com.jfinal.kit.JsonKit;
import com.jfinal.plugin.activerecord.Db;
import com.jfinal.plugin.activerecord.Record;
import com.pthink.cloudapp.commons.db.ColumnUtil;
import com.pthink.cloudapp.commons.exception.RFrame;
import com.pthink.cloudapp.commons.exception.RWarn;
import com.pthink.cloudapp.commons.log.Logs;
import com.pthink.cloudapp.commons.page.SimplePage;
import com.pthink.cloudapp.service.procedure.TradeInfo;
import com.pthink.cloudapp.standard.abstracts.Atom;
import com.pthink.cloudapp.stereotypes.Component;
import com.pthink.cloudapp.stereotypes.Item;
import com.pthink.cloudapp.stereotypes.Modified;
import com.pthink.cloudapp.stereotypes.Parameter;
import com.pthink.cloudapp.utils.TradeUtils;
import com.pthink.cloudapp.utils.Utility;

import java.util.List;

/**
 * Created by macsonLenovo on 2016-8-22.
 */
@Component(
        tradeCode = "1001",
        status = Component.Status.Run,
        internal = false,
        tradeName = "ActiveDb测试",
        author = "phy",
        comment = "ActiveDb测试",
        createDate = "2016/08/22",
        params = {
                @Parameter(classify = "查询", demo = "1001",
                        inputs = {
                                @Item(nullable = Item.Nullable.NO, id = "rq", name = "请求类型", type = Item.Type.INT, explain = "用户请求类型，默认1表示机器时间、2表示数据库时间、3表示查询一个结果集"),
                                @Item(nullable = Item.Nullable.NO, id = "userid", name = "用户ID", type = Item.Type.STRING, explain = "用户ID"),
                                @Item(nullable = Item.Nullable.YES, id = "username", name = "用户名称", type = Item.Type.STRING, explain = "用户名称"),
                                @Item(nullable = Item.Nullable.YES, id = "userip", name = "用户IP", type = Item.Type.STRING, explain = "用户IP")
                        },
                        outputs = {
                                @Item(nullable = Item.Nullable.YES, id = "r01", name = "服务器时间", type = Item.Type.STRING, explain = "服务器时间"),
                                @Item(nullable = Item.Nullable.YES, id = "r02", name = "用户IP", type = Item.Type.STRING, explain = "用户IP"),
                                @Item(nullable = Item.Nullable.NO, id = "c", name = "返回码", type = Item.Type.STRING, explain = "返回码"),
                                @Item(nullable = Item.Nullable.NO, id = "m", name = "说明", type = Item.Type.STRING, explain = "返回码说明")
                        }
                ),
                @Parameter(classify = "设置时间", demo = "1001",
                        inputs = {
                                @Item(nullable = Item.Nullable.YES, id = "usertime", name = "用户请求时间", type = Item.Type.STRING, explain = "用户请求时间"),
                                @Item(nullable = Item.Nullable.YES, id = "userip", name = "用户IP", type = Item.Type.STRING, explain = "用户IP")
                        },
                        outputs = {
                                @Item(nullable = Item.Nullable.NO, id = "c", name = "返回码", type = Item.Type.STRING, explain = "返回码"),
                                @Item(nullable = Item.Nullable.NO, id = "m", name = "说明", type = Item.Type.STRING, explain = "返回码说明")
                        }
                )
        },
        modified = {@Modified})
public class F1001 extends Atom {
    @Override
    public boolean atomicTransaction(TradeInfo tradeInfo) {

        boolean result = false;
        String tradeCode = tradeInfo.tradeCode();
        Logs.log().debug("Begin request, TradeCode[{}], clientIp=[{}]", tradeCode, tradeInfo.getConninfo().getRemoteIp());
        try {
            //this.beginTransaction();
            tradeInfo.wrap2First(RFrame.entity);
            int reqType = tradeInfo.getInt("rq");
            String userid = tradeInfo.getString("userid");
            String userName = tradeInfo.getString("username");
            String userIP = tradeInfo.getString("userip");

            if (Utility.isEmpty(userid)) {
                throw new RWarn(RWarn.MSG_99997, "userid不能为空");
            }
            if (Utility.isEmpty(reqType)) {
                throw new RWarn(RWarn.MSG_99997, "reqType不能为空");
            }
            //<outputs name=defaultout>
            tradeInfo.put("r02", userIP);

            if (getResult(reqType, tradeInfo)) {
                tradeInfo.putReason(RWarn.MSG_00000, "调用成功");
            }
            //</outputs>
            result = true;
        } catch (RWarn e) {
            throw e;
        } catch (Exception e) {
            e.printStackTrace();
            Logs.log().error("Failure request, TradeCode[{}] , TradeName [{}], err=[{}]", tradeCode, tradeInfo.getAtomInfo().getTradeName(), e.getCause().getMessage());
            throw new RWarn(RWarn.MSG_90010, tradeCode, tradeInfo.getAtomInfo().getTradeName());
        }

        Logs.log().debug("Success TradeCode[{}]", tradeCode);
        return result;
    }

    private boolean getResult(int reqType, TradeInfo tradeInfo) {
        List<Record> customers = Db.find("select * from T_DEPARTMENT limit 0,20");
        SimplePage pager = TradeUtils.getEntity(tradeInfo, SimplePage.class, RFrame.pager);
        pager.setTotalItems(customers.size());
        tradeInfo.put("pager", pager);
        tradeInfo.put("columns", ColumnUtil.getColumnList("T_DEPARTMENT", customers.get(0).getColumnNames()));
        tradeInfo.put("result", JsonKit.toJson(customers));
        return true;
    }
}

```



详细的代码编写说明请参看 《[如何开发一个新的BU](/chapter2/section2.md)》

