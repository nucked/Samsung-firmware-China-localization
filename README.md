# 实现Samsung非国行固件本地化功能

**文中只实现了部分功能，剩下的功能还在寻找发现中，你们也可以帮助一起完善。**

文中提到的KOO，CHC均为Region代码，可以根据您手机的版本不同自行变更。
##### 修复韩版刷其他版本官方固件蓝牙问题
复制韩版ROM文件到手机
```
/vendor/firmware/bcm4375B1_semco.hcd
/vendor/firmware/bcm4375B1_semco_sem.hcd
```

替换CHC的`customer.xml，omc.info`文件

修改
`/optics/configs/carriers/cscfeature.xml`,需要使用[OMC_Decoder-Encoder](https://github.com/Yoanf26/OMC_Decoder_Encoder_by_Yoanf26)解密

##### 把文本开头的代码全部换成国行的代码

```
  <Version>ED00009</Version>
  <Country>CHINA</Country>
  <CountryISO>CN</CountryISO>
  <SalesCode>CHC</SalesCode>

```

```
把KOO全部改成CHC
```
##### 加入黄页

```
<CscFeature_Contact_ConfigForYellowPage>SHOW</CscFeature_Contact_ConfigForYellowPage>
```

复制黄页app 
```\system\system\priv-app\SamsungYellowPage\SamsungYellowPage.apk```

到自己自己ROM/手机

##### 设置日历颜色
```
<CscFeature_Calendar_SetColorOfDays>XXXXXBR</CscFeature_Calendar_SetColorOfDays>
```

##### 启用中国假期日历

```
<CscFeature_Calendar_EnableLocalHolidayDisplay>CHINA</CscFeature_Calendar_EnableLocalHolidayDisplay>
```
##### 启用农历

```
<CscFeature_Calendar_EnableLunar>TRUE</CscFeature_Calendar_EnableLunar>
```



##### 通话中使用摄像头

```
<CscFeature_Camera_EnableCameraDuringCall>TRUE</CscFeature_Camera_EnableCameraDuringCall>
```


##### 启用自动排列图标：

```
<CscFeature_Launcher_SupportAutoIconAlign>TRUE</CscFeature_Launcher_SupportAutoIconAlign>
```


#### 启用通话录音：

```
<CscFeature_VoiceCall_ConfigRecording>RecordingAllowed</CscFeature_VoiceCall_ConfigRecording>
```


#### 天气本地化
```
<CscFeature_Weather_ConfigCpType>CMA</CscFeature_Weather_ConfigCpType>
<CscFeature_Weather_ConfigDefRefreshInterval>3</CscFeature_Weather_ConfigDefRefreshInterval>
<CscFeature_Weather_ConfigDefTempUnit>1</CscFeature_Weather_ConfigDefTempUnit>
```

##### 相机快门声音开关

```
<CscFeature_Camera_ShutterSoundMenu>TRUE</CscFeature_Camera_ShutterSoundMenu>
```


##### SyncMl保留，其余全部删掉

```
<CscFeature_SyncML_ConfigDevicePreId>IMEI</CscFeature_SyncML_ConfigDevicePreId>
```


##### 运营商版本

```
<CscFeature_SystemUI_ConfigOpBranding5GIcon>5GAvailable,RRCStateCheck,UseOneShapedIcon,UseDisplayTimer</CscFeature_SystemUI_ConfigOpBranding5GIcon>
<CscFeature_SystemUI_ConfigOpBrandingForIndicatorIcon>CHC</CscFeature_SystemUI_ConfigOpBrandingForIndicatorIcon>
<CscFeature_SystemUI_ConfigOpBrandingForQuickSettingLabel>CHC</CscFeature_SystemUI_ConfigOpBrandingForQuickSettingLabel>
<CscFeature_SystemUI_ConfigOpBrandingQuickSettingIcon>CHC</CscFeature_SystemUI_ConfigOpBrandingQuickSettingIcon>
```

##### Volte

```
<CscFeature_VoiceCall_ConfigOpStyleForVolte>VolteCtc,CTC_VOLTE,wait_for_volte_regi_in_airplane_mode_ctc</CscFeature_VoiceCall_ConfigOpStyleForVolte>
```

##### 加入网速显示

```
<CscFeature_Setting_SupportRealTimeNetworkSpeed>TRUE</CscFeature_Setting_SupportRealTimeNetworkSpeed>
```



##### 闹钟响起前开机

```
<CscFeature_Clock_EnableAutoPowerOnOffMenu>TRUE</CscFeature_Clock_EnableAutoPowerOnOffMenu>
<CscFeature_Clock_ExclusiveEnablingAutoPowerSetting>TRUE</CscFeature_Clock_ExclusiveEnablingAutoPowerSetting>

```

删掉
##### TTY模式:(没啥篮子用)
```
<CscFeature_VoiceCall_SupportTTY>TRUE</CscFeature_VoiceCall_SupportTTY>
```


##### 电话相关

```
省事可以把cscfeature.xml和cscfeature_network.xml里面”CscFeature_VoiceCall“的文本全部替换
```


##### Bixby识屏移植 via:酷安@三星忠实头号黑粉

复制国行ROM
```
\system\system\priv-app\BixbyTouch
\system\system\etc\sysconfig\bixbytouchapp.xml
\system\system\etc\permissions\privapp-permissions-com.samsung.android.bixbytouch.xml
```



`\vendor\etc\floating_feature.xml`文件里面加入
```
<SEC_FLOATING_FEATURE_COMMON_SUPPORT_BIXBY_TOUCH>TRUE</SEC_FLOATING_FEATURE_COMMON_SUPPORT_BIXBY_TOUCH>
```

##### 加入自动开关机功能
`\vendor\etc\floating_feature.xml`文件里面加入
```
<SEC_FLOATING_FEATURE_SETTINGS_SUPPORT_AUTO_POWER_ON_OFF>TRUE</SEC_FLOATING_FEATURE_SETTINGS_SUPPORT_AUTO_POWER_ON_OFF>
```

##### 加入来电归属地
把国行ROM

```
\system\system\priv-app\PhoneNumberLocatorService\PhoneNumberLocatorService.apk
\system\system\etc\sysconfig\phonenumberlocatorservice.xml
\system\system\etc\permissions\privapp-permissions-com.sgmc.phonenumberlocatorservice.xml
```


复制到相同目录

###### 智慧主页

删除
`system\system\app\MinusOnePage\MinusOnePage.apk`

##### Bixby主页
```
\system\system\priv-app\BixbyHomeCN_Disable
\system\system\etc\permissions\privapp-permissions-bixbyhomecn.xml
```
复制进手机目录

##### 加入智能管理器

删除/备份

```
\system\priv-app\SmartManager_v5\SmartManager_v5.apk
\system\priv-app\SmartManager_v6_DeviceSecurity\SmartManager_v6_DeviceSecurity.apk
```
复制国行ROM里面的

```
\system\system\priv-app\SmartManager_v6_DeviceSecurity_CN
\system\system\priv-app\SmartManagerCN
```
到相同目录
修改`\vendor\etc\floating_feature.xml`
把SMARTMANAGER_CONFIG_PACKAGE_NAME段改成

```
<SEC_FLOATING_FEATURE_SMARTMANAGER_CONFIG_PACKAGE_NAME>com.samsung.android.sm_cn</SEC_FLOATING_FEATURE_SMARTMANAGER_CONFIG_PACKAGE_NAME>
```
把SECURITY_CONFIG_DEVICEMONITOR_PACKAGE_NAME段改成
```
<SEC_FLOATING_FEATURE_SECURITY_CONFIG_DEVICEMONITOR_PACKAGE_NAME>com.samsung.android.sm.devicesecurity.tcm</SEC_FLOATING_FEATURE_SECURITY_CONFIG_DEVICEMONITOR_PACKAGE_NAME>
```
复制国行ROM  
```
\system\system\etc\permissions\privapp-permissions-com.samsung.android.sm_cn.xml
\system\system\etc\permissions\privapp-permissions-com.samsung.android.sm.devicesecurity.tcm_v6.xml
```
文件到相同目录


##### 加入骚扰拦截
复制国行ROM
```
\system\system\etc\permissions\privapp-permissions-com.sec.android.app.firewall.xml
\system\system\priv-app\Firewall
```
到相同目录


##### 加入应用程序锁定
复制复制国行ROM

 ```
 \system\system\priv-app\AppLock
 \system\system\etc\permissions\privapp-permissions-com.samsung.android.applock.xml
 ```

到相同目录

修改`\prism\etc\carriers\single\KOO\enforceskippingpackages.txt`删除里面的

```
AppLock.apk
```



##### 更改SPen翻译为百度翻译
修改`/optics/configs/carriers/cscfeature.xml`加入
```
<CscFeature_SPen_ConfigDefTranslatorSolution>Baidu</CscFeature_SPen_ConfigDefTranslatorSolution>
```