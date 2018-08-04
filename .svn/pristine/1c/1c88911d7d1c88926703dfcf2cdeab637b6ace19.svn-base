<#include "/macro.include"/>
<#include "/custom.include">
<#include "/java_copyright.include">
<#assign className = table.className>   
<#assign classNameFirstLower = className?uncap_first>   
<#assign classNameLowerCase = className?lower_case>   
<#assign pkJavaType = table.idColumn.javaType>   

package ${basepackage}.${classNameFirstLower}.controller;



import java.util.Date;

import javax.servlet.http.HttpServletRequest;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.WebDataBinder;
import org.springframework.web.bind.annotation.InitBinder;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;
import org.springframework.web.context.request.WebRequest;

import com.minstone.common.dbutil.DBManager;
import com.minstone.common.model.UserInfo;
import com.minstone.common.util.CommonConstants;
import com.minstone.common.util.ControllerException;
import com.minstone.common.util.MyWebBindingInitializer;
import com.minstone.common.util.ParamUtil;
import com.minstone.common.util.Tools;
import com.minstone.znnj.common.helper.UserHelper;
import com.minstone.znnj.common.web.jsontip.JsonTips;

import ${basepackage}.${classNameFirstLower}.service.${className}Service;
import ${basepackage}.${classNameFirstLower}.model.${className};

/**
 * ${wzz_functionName} controller 
 * @author ${wzz_classAuthor}
 * @version ${wzz_classVersion}
 */


@Controller
public class ${className}Controller {
	
	/**
	 * this loger  can be used by controller in anywhere . wzz
	 */
	private Logger log = LoggerFactory.getLogger(${className}Controller.class);
	
	@Autowired
	private ${className}Service ${classNameFirstLower}Service;
	
	@Autowired
	private MyWebBindingInitializer myWebBindingInitializer;
	
	@InitBinder
	public void initBinder1(WebDataBinder binder, WebRequest request) {
		myWebBindingInitializer.initBinder(binder, request);
	}
	
	/**
	 * 获取  ${wzz_functionName}  列表信息
	 * @param request
	 * @return
	 */
	@RequestMapping(value = "/${classNameFirstLower}/list")
	public String list(HttpServletRequest request) {
//		try {
//			${classNameFirstLower}Service.getList(request);
//		} catch (Exception e) {
//			throw new ControllerException(ControllerException.C_MSG, e);
//		}
		return "${wzz_moduleName}/${classNameFirstLower}/list_${classNameFirstLower}";
	}
	
	/**
	 * 新增 
	 * @return
	 */
	@RequestMapping(value = "/${classNameFirstLower}/add")
	public String add(HttpServletRequest request,Model model){
		${className} ${classNameFirstLower}= new ${className}();
        try {
    		Long id = DBManager.getCommonSeq(ParamUtil.getCurrentUser(request));
    		${classNameFirstLower}.set${table.idColumn.columnName}(id);
		} catch (Exception e) {
			throw new ControllerException(ControllerException.C_MSG, e);
		}
		model.addAttribute("${classNameFirstLower}",${classNameFirstLower});
		model.addAttribute("operateType","add");
		return "${wzz_moduleName}/${classNameFirstLower}/form_${classNameFirstLower}";
	}
	
	/**
	 * 编辑
	 * @return
	 */
	@RequestMapping(value = "/${classNameFirstLower}/edit/{id}")
	public String edit(HttpServletRequest request,Model model,@PathVariable Long id){
		${className} ${classNameFirstLower}= null;
		try {
			${classNameFirstLower} = this.${classNameFirstLower}Service.getById(id);
		} catch (Exception e) {
			throw new ControllerException(ControllerException.C_MSG, e);
		}
		model.addAttribute("${classNameFirstLower}",${classNameFirstLower});
		model.addAttribute("operateType","edit");
		return "${wzz_moduleName}/${classNameFirstLower}/form_${classNameFirstLower}";
	}
	
	/**
	 * 保存
	 * @return
	 */
	@ResponseBody
	@RequestMapping(value = "/${classNameFirstLower}/save")
	public JsonTips save(${className} ${classNameFirstLower}, HttpServletRequest request , Model model){
		JsonTips tips =  new JsonTips();
		boolean flag = false;
		try {
			String operateType = ParamUtil.getString(request, "operateType");
			UserInfo userInfo  = UserHelper.getCurrentUser(request);
			String curUserCode = ParamUtil.getCurrentUser(request);
			String systemCode  = CommonConstants.SYS_FLAG;//系统标识
			String areaCode    = CommonConstants.getAreaCode(curUserCode);//区域代码
			String orgCode     = CommonConstants.getOrgCode(curUserCode);//单位代码
			//-- 这段代码根据 业务需求 自行修改   begin --//
			if("add".equals(operateType)){
				${classNameFirstLower}.setCreaterCode(userInfo.getUserCode());
				${classNameFirstLower}.setCreaterName(userInfo.getUserName());
				${classNameFirstLower}.setCreateTime(new Date());
			}
			if("edit".equals(operateType)){
				${classNameFirstLower}.setUpdaterCode(userInfo.getUserCode());
				${classNameFirstLower}.setUpdaterName(userInfo.getUserName());
				${classNameFirstLower}.setUpdateTime(new Date());
			}
			${classNameFirstLower}.setSystemCode(systemCode);
			${classNameFirstLower}.setAreaCode(areaCode);
			${classNameFirstLower}.setOrgCode(orgCode);
			//-- 这段代码根据 业务需求 自行修改   end  --//
			
			flag = this.${classNameFirstLower}Service.saveOrUpdate(${classNameFirstLower},operateType);
		} catch (Exception e) {
			throw new ControllerException(ControllerException.C_MSG, e);
		}
		tips.setFlag(flag);
		return tips;	
	}
	
	/**
	 * 删除
	 * @return
	 */
	@ResponseBody
	@RequestMapping(value = "/${classNameFirstLower}/delete/{ids}")
	public JsonTips delete(HttpServletRequest request,@PathVariable String ids){
		JsonTips tips =  new JsonTips();
		boolean flag = false;
		try {
			flag = this.${classNameFirstLower}Service.delete${className}(ids);
		} catch (Exception e) {
			throw new ControllerException(ControllerException.C_MSG, e);
		}
		tips.setFlag(flag);
		return tips;
	}
	
}
