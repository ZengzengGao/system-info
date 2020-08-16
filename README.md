# system-info
基于python3的linux和windows系统信息api

linux and windows system information api

### based on: python3.8

所有api均支持linux和windows

All apis support linux and windows

# api列表：

```
CpuConstants
ExecShellUnix
GetBootTime
GetCpuConstants
GetCpuInfo
GetDiskInfo
GetDiskInfoUnix
GetDiskInfoWindows
GetErrorInfo
GetFullSystemData
GetIoRead
GetIoReadWrite
GetIoWrite
GetLoadAverage
GetMemInfo
GetMemInfoUnix
GetMemInfoWindows
GetNetWork
GetRegValue
GetSystemInfo
GetSystemVersion
GetSystemVersionUnix
GetSystemVersionWindows
ToSizeInt
ToSizeString
UNIX
cpuConstants
md5
readFile
```


# api说明：

## 当前系统网络使用情况：上传下载速率，收发包
```python
GetNetWork()
```
#### both
```python
{
	'up': 1.54,
	'down': 0.37,
	'upTotal': 87688289,
	'downTotal': 336439316,
	'downPackets': 397399,
	'upPackets': 262468
}
```
 
## 当前系统磁盘IO情况：IO读写
```python
GetIoReadWrite()
```
#### both
```python
{'write': 1003332, 'read': 1466368}
```

## 当前系统CPU常量
```python
GetCpuConstants()
```

#### windows
```python
{'cpu_count': 1, 'cpu_name': 'AMD Ryzen 5 2500U with Radeon Vega Mobile Gfx  ', 'cpu_core': 4, 'cpu_threads': 8}
```

#### linux
```python
{'cpu_count': 1, 'cpu_name': 'Intel(R) Xeon(R) Platinum 8269CY CPU @ 2.50GHz', 'cpu_core': 1, 'cpu_threads': 1}
```

## 当前系统CPU信息、使用率
```python
GetCpuInfo()
```

#### windows
```python
{
	'used': 17.2,
	'used_list': [23.8, 12.2, 19.6, 10.2, 20.3, 6.2, 12.6, 30.3],
	'cpu_count': 1,
	'cpu_name': 'AMD Ryzen 5 2500U with Radeon Vega Mobile Gfx  ',
	'cpu_core': 4,
	'cpu_threads': 8
}
```

#### linux
```python
{
	'used': 2.0,
	'used_list': [3.4],
	'cpu_count': 1,
	'cpu_name': 'Intel(R) Xeon(R) Platinum 8269CY CPU @ 2.50GHz',
	'cpu_core': 1,
	'cpu_threads': 1
}
```

## 当前系统负载信息
```python
GetLoadAverage()
```

#### windows
```python
{
	'one': 0,
	'five': 0,
	'fifteen': 0,
	'max': 16,
	'limit': 16,
	'safe': 12.0
}
```

#### linux
```python
{
	'one': 0.46,
	'five': 0.18,
	'fifteen': 0.14,
	'max': 2,
	'limit': 2,
	'safe': 1.5
}
```

## 当前系统内存使用情况（linux比windows多了cached和buffers）
```python
GetMemInfo()
```
#### windows
```python
{
	'memTotal': 7069,
	'memFree': 1202,
	'memRealUsed': 5866,
	'menUsedPercent': '82.98'
}
```

#### linux
```python
{
	'memTotal': 1838,
	'memFree': 181,
	'memBuffers': 25,
	'memCached': 448,
	'memRealUsed': 1184,
	'memUsedPercent': 64.41784548422198
}
```

## 当前系统磁盘信息
```python
GetDiskInfo()
```

#### windows
```python
[{'path': 'C:/',
  'size': {'total': 85899341824,
   'used': 84512485376,
   'free': 1386856448,
   'percent': 98.4},
  'fstype': 'NTFS',
  'inodes': False},
 {'path': 'D:/',
  'size': {'total': 413524815872,
   'used': 367597920256,
   'free': 45926895616,
   'percent': 88.9},
  'fstype': 'NTFS',
  'inodes': False}]
```

#### linux
```python
[{
	'path': '/',
	'size': ['50G', '16G', '32G', '33%'],
	'inodes': ['3276800', '261498', '3015302', '8%']
}]
```

  
## 获取系统注册表信息（仅windows可用）
```python
GetRegValue(key: str, subkey: str, value: str)
```
```python
    '''
  获取系统注册表信息

  Parameters
  ----------
  key : str
      类型.
  subkey : str
      路径.
  value : str
      key.

  Returns
  -------
  value : Any
      DESCRIPTION.

  '''
  ```

## 获取系统版本信息
```python
GetSystemVersion()
```

#### windows
```python
Windows 10 Home China (build 18362) x64 (Py3.8.5)
```

#### linux
```python
CentOS  7.6.1810(Py 3.8.5)
```

## 获取系统启动时间及运行时间
```python
GetBootTime()
```

#### both
```python
{'timestamp': 1597574445.835271,
 'runtime': 33396.16829442978,
 'datetime': '2020-08-17 03:57:22'}
```

## 获取全部系统信息
```python
GetFullSystemData()
```

#### windows
```python
{
	'cpu': {
		'used': 16.0,
		'used_list': [29.0, 16.4, 30.5, 13.9, 28.1, 16.8, 24.0, 26.7],
		'cpu_count': 1,
		'cpu_name': 'AMD Ryzen 5 2500U with Radeon Vega Mobile Gfx  ',
		'cpu_core': 4,
		'cpu_threads': 8
	},
	'load': {
		'one': 0,
		'five': 0,
		'fifteen': 0,
		'max': 16,
		'limit': 16,
		'safe': 12.0
	},
	'mem': {
		'memTotal': 7069,
		'memFree': 1181,
		'memRealUsed': 5888,
		'menUsedPercent': '83.29'
	},
	'disk': [{
		'path': 'C:/',
		'size': {
			'total': 85899341824,
			'used': 84515794944,
			'free': 1383546880,
			'percent': 98.4
		},
		'fstype': 'NTFS',
		'inodes': False
	}, {
		'path': 'D:/',
		'size': {
			'total': 413524815872,
			'used': 367597862912,
			'free': 45926952960,
			'percent': 88.9
		},
		'fstype': 'NTFS',
		'inodes': False
	}],
	'network': {
		'up': 1.84,
		'down': 2.69,
		'upTotal': 92363508,
		'downTotal': 342344006,
		'downPackets': 409006,
		'upPackets': 271275
	},
	'io': {
		'write': 1277171,
		'read': 38696960
	},
	'boot': {
		'timestamp': 1597574445.966399,
		'runtime': 34064.19006037712,
		'datetime': '2020-08-17 04:08:30'
	},
	'time': 1597608510.1564593
}
```

#### linux
```python
{
	'cpu': {
		'used': 6.0,
		'used_list': [3.4],
		'cpu_count': 1,
		'cpu_name': 'Intel(R) Xeon(R) Platinum 8269CY CPU @ 2.50GHz',
		'cpu_core': 1,
		'cpu_threads': 1
	},
	'load': {
		'one': 0.59,
		'five': 0.49,
		'fifteen': 0.28,
		'max': 2,
		'limit': 2,
		'safe': 1.5
	},
	'mem': {
		'memTotal': 1838,
		'memFree': 180,
		'memBuffers': 26,
		'memCached': 448,
		'memRealUsed': 1184,
		'memUsedPercent': 64.41784548422198
	},
	'disk': [{
		'path': '/',
		'size': ['50G', '16G', '32G', '33%'],
		'inodes': ['3276800', '261498', '3015302', '8%']
	}],
	'network': {
		'up': 0.0,
		'down': 0.0,
		'upTotal': 606720149,
		'downTotal': 479946863,
		'downPackets': 1431369,
		'upPackets': 1305962
	},
	'io': {
		'write': 0,
		'read': 0
	},
	'boot': {
		'timestamp': 1597435339.0,
		'runtime': 175312.03097391129,
		'datetime': '2020-08-17 04:44:11'
	},
	'time': 1597610651.0309963
}
```

## Author
### Pure-Peace
  
```
systemInfo.py
```

```python
# -*- coding: utf-8 -*-
'''
@name: 系统信息 / SystemInfo
@author: PurePeace
@time: 2020年8月17日
@version: 0.1
'''

from typing import List, Dict, Any

import os
import time
import psutil
import platform
import hashlib
import re
import sys


from cachelib import SimpleCache
cache = SimpleCache()


UNIX: bool = os.name == 'posix'
SYS: str = platform.system()


class CpuConstants:
    def __init__(self):
        '''
        初始化CPU常量（多平台）
        Returns
        -------
        self.
        '''
        self.WMI = None
        self.initialed: bool = False
        self.cpuList: list = [] # windows only

        self.cpuCount: int = 0 # 物理cpu数量
        self.cpuCore: int = 0 # cpu物理核心数
        self.cpuThreads: int = 0 # cpu逻辑核心数
        self.cpuName: str = '' # cpu型号

        self.Update(True)


    def Update(self, update: bool = False) -> None:
        '''
        更新cpu数据
        Returns
        -------
        None.
        '''
        if UNIX: self.GetCpuConstantsUnix(update)
        else: self.GetCpuConstantsWindows(update)

        self.initialed: bool = True


    @property
    def getDict(self) -> Dict[int, str]:
        '''
        以字典格式获取当前cpu常量
        Returns
        -------
        Dict[int, str]
            DESCRIPTION.
        '''
        if not self.initialed: self.Update()
        return {
            'cpu_count': self.cpuCount,
            'cpu_name': self.cpuName,
            'cpu_core': self.cpuCore,
            'cpu_threads': self.cpuThreads
        }


    def GetCpuConstantsUnix(self, update: bool = False) -> None:
        '''
        获取unix下的cpu信息
        Parameters
        ----------
        update : bool, optional
            DESCRIPTION. The default is False.
        Returns
        -------
        None
            DESCRIPTION.
        '''
        if update or not self.initialed:
            ids: list = re.findall("physical id.+", readFile('/proc/cpuinfo'))

            # 物理cpu个数
            self.cpuCount: int = len(set(ids))

            # cpu型号（名称）
            self.cpuName: str = self.getCpuTypeUnix()


            self.GetCpuConstantsBoth()


    def InitWmi(self) -> None:
        '''
        初始化wmi（for windows）
        Returns
        -------
        None
            DESCRIPTION.
        '''
        import wmi
        self.WMI = wmi.WMI()


    def GetCpuConstantsBoth(self, update: bool = False) -> None:
        '''
        获取多平台共用的cpu信息
        Parameters
        ----------
        update : bool, optional
            强制更新数据. The default is False.
        Returns
        -------
        None
            DESCRIPTION.
        '''
        if update or not self.initialed:

            # cpu逻辑核心数
            self.cpuThreads: int = psutil.cpu_count()

            # cpu物理核心数
            self.cpuCore: int = psutil.cpu_count(logical=False)


    def GetCpuConstantsWindows(self, update: bool = False) -> None:
        '''
        获取windows平台的cpu信息
        Parameters
        ----------
        update : bool, optional
            强制更新数据. The default is False.
        Returns
        -------
        None
            DESCRIPTION.
        '''
        if update or not self.initialed:

            # 初始化wmi
            if self.WMI == None: self.InitWmi()

            # cpu列表
            self.cpuList: list = self.WMI.Win32_Processor()

            # 物理cpu个数
            self.cpuCount: int = len(self.cpuList)

            # cpu型号（名称）
            self.cpuName: str = self.cpuList[0].Name


            self.GetCpuConstantsBoth()


    @staticmethod
    def getCpuTypeUnix() -> str:
        '''
        获取CPU型号（unix）
        Returns
        -------
        str
            CPU型号.
        '''
        cpuinfo: str = readFile('/proc/cpuinfo')
        rep: str = 'model\s+name\s+:\s+(.+)'
        tmp = re.search(rep,cpuinfo,re.I)
        cpuType: str = ''
        if tmp:
            cpuType: str = tmp.groups()[0]
        else:
            cpuinfo = ExecShellUnix('LANG="en_US.UTF-8" && lscpu')[0]
            rep = 'Model\s+name:\s+(.+)'
            tmp = re.search(rep,cpuinfo,re.I)
            if tmp: cpuType = tmp.groups()[0]
        return cpuType


def GetCpuInfo(interval: int = 1) -> Dict[str, Any]:
    '''
    获取CPU信息
    Parameters
    ----------
    interval : int, optional
        DESCRIPTION. The default is 1.
    Returns
    -------
    Dict[float, list, dict]
        DESCRIPTION.
    '''
    time.sleep(0.5)


    # cpu总使用率
    used: float = psutil.cpu_percent(interval)

    # 每个逻辑cpu使用率
    usedList: List[float] = psutil.cpu_percent(percpu=True)


    return {'used': used, 'used_list': usedList, **cpuConstants.getDict}


def readFile(filename: str) -> str:
    '''
    读取文件内容
    Parameters
    ----------
    filename : str
        文件名.
    Returns
    -------
    str
        文件内容.
    '''
    try:
        with open(filename, 'r', encoding='utf-8') as file: return file.read()
    except:
        pass

    return ''


def GetLoadAverage() -> dict:
    '''
    获取服务器负载状态（多平台）
    Returns
    -------
    dict
        DESCRIPTION.
    '''
    try: c: list = os.getloadavg()
    except: c: list = [0,0,0]
    data: dict = {i: c[idx] for idx, i in enumerate(('one', 'five', 'fifteen'))}
    data['max'] = psutil.cpu_count() * 2
    data['limit'] = data['max']
    data['safe'] = data['max'] * 0.75
    return data


def GetMemInfo() -> dict:
    '''
    获取内存信息（多平台）
    Returns
    -------
    dict
        DESCRIPTION.
    '''
    if UNIX: return GetMemInfoUnix()
    return GetMemInfoWindows()


def GetMemInfoUnix() -> Dict[str, int]:
    '''
    获取内存信息（unix）
    Returns
    -------
    dict
        DESCRIPTION.
    '''
    mem = psutil.virtual_memory()
    memInfo: dict = {
        'memTotal': ToSizeInt(mem.total, 'MB'),
        'memFree': ToSizeInt(mem.free, 'MB'),
        'memBuffers': ToSizeInt(mem.buffers, 'MB'),
        'memCached': ToSizeInt(mem.cached, 'MB'),
    }
    memInfo['memRealUsed'] = \
        memInfo['memTotal'] - \
        memInfo['memFree'] - \
        memInfo['memBuffers'] - \
        memInfo['memCached']

    memInfo['memUsedPercent'] = memInfo['memRealUsed'] / memInfo['memTotal'] * 100

    return memInfo


def GetMemInfoWindows() -> dict:
    '''
    获取内存信息（windows）
    Returns
    -------
    dict
        DESCRIPTION.
    '''
    mem = psutil.virtual_memory()
    memInfo: dict = {
        'memTotal': ToSizeInt(mem.total, 'MB'),
        'memFree': ToSizeInt(mem.free, 'MB'),
        'memRealUsed': ToSizeInt(mem.used, 'MB'),
        'menUsedPercent': mem.used / mem.total * 100
    }

    return memInfo


def ToSizeInt(byte: int, target: str) -> int:
    '''
    将字节大小转换为目标单位的大小
    Parameters
    ----------
    byte : int
        int格式的字节大小（bytes size）
    target : str
        目标单位，str.
    Returns
    -------
    int
        转换为目标单位后的字节大小.
    '''
    return int(byte/1024**(('KB','MB','GB','TB').index(target) + 1))


def ToSizeString(byte: int) -> str:
    '''
    获取字节大小字符串
    Parameters
    ----------
    byte : int
        int格式的字节大小（bytes size）.
    Returns
    -------
    str
        自动转换后的大小字符串，如：6.90 GB.
    '''
    units: tuple = ('b','KB','MB','GB','TB')
    re = lambda: '{:.2f} {}'.format(byte, u)
    for u in units:
        if byte < 1024: return re()
        byte /= 1024
    return re()


def GetDiskInfo() -> list:
    '''
    获取磁盘信息（多平台）
    Returns
    -------
    list
        列表.
    '''
    try:
        if UNIX: return GetDiskInfoUnix()
        return GetDiskInfoWindows()
    except Exception as err:
        print('获取磁盘信息异常（unix: {}）：'.format(UNIX), err)
        return []


def GetDiskInfoWindows() -> list:
    '''
    获取磁盘信息Windows
    Returns
    -------
    diskInfo : list
        列表.
    '''
    diskIo: list = psutil.disk_partitions()
    diskInfo: list = []
    for disk in diskIo:
        tmp: dict = {}
        try:
            tmp['path'] = disk.mountpoint.replace("\\","/")
            usage = psutil.disk_usage(disk.mountpoint)
            tmp['size'] = {
                'total': usage.total,
                'used': usage.used,
                'free': usage.free,
                'percent': usage.percent
            }
            tmp['fstype'] = disk.fstype
            tmp['inodes'] = False
            diskInfo.append(tmp)
        except:
            pass
    return diskInfo


def GetDiskInfoUnix() -> list:
     '''
    获取硬盘分区信息（unix）
    Returns
    -------
    list
        DESCRIPTION.
    '''
     temp: list = (
         ExecShellUnix("df -h -P|grep '/'|grep -v tmpfs")[0]).split('\n')
     tempInodes: list = (
         ExecShellUnix("df -i -P|grep '/'|grep -v tmpfs")[0]).split('\n')
     diskInfo: list = []
     n: int = 0
     cuts: list = [
         '/mnt/cdrom',
         '/boot',
         '/boot/efi',
         '/dev',
         '/dev/shm',
         '/run/lock',
         '/run',
         '/run/shm',
         '/run/user'
     ]
     for tmp in temp:
         n += 1
         try:
             inodes: list = tempInodes[n-1].split()
             disk: list = tmp.split()
             if len(disk) < 5: continue
             if disk[1].find('M') != -1: continue
             if disk[1].find('K') != -1: continue
             if len(disk[5].split('/')) > 10: continue
             if disk[5] in cuts: continue
             if disk[5].find('docker') != -1: continue
             arr = {}
             arr['path'] = disk[5]
             tmp1 = [disk[1],disk[2],disk[3],disk[4]]
             arr['size'] = tmp1
             arr['inodes'] = [inodes[1],inodes[2],inodes[3],inodes[4]]
             diskInfo.append(arr)
         except Exception as ex:
             print('信息获取错误：', str(ex))
             continue
     return diskInfo



def md5(strings: str) -> str:
    '''
    生成md5
    Parameters
    ----------
    strings : TYPE
        要进行hash处理的字符串
    Returns
    -------
    str[32]
        hash后的字符串.
    '''

    m = hashlib.md5()
    m.update(strings.encode('utf-8'))
    return m.hexdigest()


def GetErrorInfo() -> str:
    '''
    获取traceback中的错误
    Returns
    -------
    str
        DESCRIPTION.
    '''
    import traceback
    errorMsg = traceback.format_exc()
    return errorMsg


def ExecShellUnix(cmdstring: str, shell=True):
    '''
    执行Shell命令（Unix）
    Parameters
    ----------
    cmdstring : str
        DESCRIPTION.
    shell : TYPE, optional
        DESCRIPTION. The default is True.
    Returns
    -------
    a : TYPE
        DESCRIPTION.
    e : TYPE
        DESCRIPTION.
    '''
    a: str = ''
    e: str = ''
    import subprocess,tempfile

    try:
        rx: str = md5(cmdstring)
        succ_f = tempfile.SpooledTemporaryFile(
            max_size = 4096,
            mode = 'wb+',
            suffix = '_succ',
            prefix = 'btex_' + rx ,
            dir = '/dev/shm'
        )
        err_f = tempfile.SpooledTemporaryFile(
            max_size = 4096,
            mode = 'wb+',
            suffix = '_err',
            prefix = 'btex_' + rx ,
            dir = '/dev/shm'
        )
        sub = subprocess.Popen(
            cmdstring,
            close_fds = True,
            shell = shell,
            bufsize = 128,
            stdout = succ_f,
            stderr = err_f
        )
        sub.wait()
        err_f.seek(0)
        succ_f.seek(0)
        a = succ_f.read()
        e = err_f.read()
        if not err_f.closed: err_f.close()
        if not succ_f.closed: succ_f.close()
    except Exception as err:
        print(err)
    try:
        if type(a) == bytes: a = a.decode('utf-8')
        if type(e) == bytes: e = e.decode('utf-8')
    except Exception as err:
        print(err)

    return a,e


def GetNetWork() -> dict:
    '''
    获取系统网络信息
    Returns
    -------
    dict
        DESCRIPTION.
    '''
    networkIo: list = [0,0,0,0]
    cache_timeout: int = 86400
    try:
        networkIo = psutil.net_io_counters()[:4]
    except:
        pass

    otime = cache.get("otime")
    if not otime:
        otime = time.time()
        cache.set('up',networkIo[0],cache_timeout)
        cache.set('down',networkIo[1],cache_timeout)
        cache.set('otime',otime ,cache_timeout)

    ntime = time.time()
    networkInfo: dict = {'up': 0, 'down': 0}
    networkInfo['upTotal']   = networkIo[0]
    networkInfo['downTotal'] = networkIo[1]
    try:
        networkInfo['up'] = round(
            float(networkIo[0] - cache.get("up")) / 1024 / (ntime - otime),
            2
        )
        networkInfo['down'] = round(
            float(networkIo[1] - cache.get("down")) / 1024 / (ntime -  otime),
            2
        )
    except:
        pass

    networkInfo['downPackets'] = networkIo[3]
    networkInfo['upPackets'] = networkIo[2]

    cache.set('up',networkIo[0],cache_timeout)
    cache.set('down',networkIo[1],cache_timeout)
    cache.set('otime', time.time(),cache_timeout)

    return networkInfo


def GetSystemInfo() -> dict:
    systemInfo: dict = {}
    systemInfo['cpu'] = GetCpuInfo()
    systemInfo['load'] = GetLoadAverage()
    systemInfo['mem'] = GetMemInfo()
    systemInfo['disk'] = GetDiskInfo()

    return systemInfo



def GetIoReadWrite() -> Dict[str, int]:
    '''
    获取系统IO读写
    Returns
    -------
    dict
        DESCRIPTION.
    '''
    ioDisk = psutil.disk_io_counters()
    ioTotal: dict = {}
    ioTotal['write'] = GetIoWrite(ioDisk.write_bytes)
    ioTotal['read'] = GetIoRead(ioDisk.read_bytes)
    return ioTotal


def GetIoWrite(ioWrite: int) -> int:
    '''
    获取IO写
    Parameters
    ----------
    ioWrite : TYPE
        DESCRIPTION.
    Returns
    -------
    int
        DESCRIPTION.
    '''
    diskWrite: int = 0
    oldWrite: int = cache.get('io_write')
    if not oldWrite:
        cache.set('io_write', ioWrite)
        return diskWrite;

    oldTime: float = cache.get('io_time')
    newTime: float = time.time()
    if not oldTime: oldTime = newTime
    ioEnd: int = (ioWrite - oldWrite)
    timeEnd: float = (time.time() - oldTime)
    if ioEnd > 0:
        if timeEnd < 1: timeEnd = 1
        diskWrite = ioEnd / timeEnd
    cache.set('io_write',ioWrite)
    cache.set('io_time',newTime)
    if diskWrite > 0: return int(diskWrite)
    return 0


def GetIoRead(ioRead):
    '''
    读取IO读
    Parameters
    ----------
    ioRead : TYPE
        DESCRIPTION.
    Returns
    -------
    TYPE
        DESCRIPTION.
    '''
    diskRead: int = 0
    oldRead: int = cache.get('io_read')
    if not oldRead:
        cache.set('io_read',ioRead)
        return diskRead;
    oldTime: float = cache.get('io_time')
    newTime: float = time.time()
    if not oldTime: oldTime = newTime
    ioEnd: int = (ioRead - oldRead)
    timeEnd: float = (time.time() - oldTime)
    if ioEnd > 0:
        if timeEnd < 1: timeEnd = 1;
        diskRead = ioEnd / timeEnd;
    cache.set('io_read', ioRead)
    if diskRead > 0: return int(diskRead)
    return 0


def GetRegValue(key: str, subkey: str, value: str) -> Any:
    '''
    获取系统注册表信息
    Parameters
    ----------
    key : str
        类型.
    subkey : str
        路径.
    value : str
        key.
    Returns
    -------
    value : Any
        DESCRIPTION.
    '''
    import winreg
    key = getattr(winreg, key)
    handle = winreg.OpenKey(key, subkey)
    (value, type) = winreg.QueryValueEx(handle, value)
    return value


def GetSystemVersion() -> str:
    '''
    获取操作系统版本（多平台）
    Returns
    -------
    str
        DESCRIPTION.
    '''
    if UNIX: return GetSystemVersionUnix()
    return GetSystemVersionWindows()


def GetSystemVersionWindows() -> str:
    '''
    获取操作系统版本（windows）
    Returns
    -------
    str
        DESCRIPTION.
    '''
    try:
        import platform
        bit: str = 'x86';
        if 'PROGRAMFILES(X86)' in os.environ: bit = 'x64'

        def get(key: str):
            return GetRegValue(
                "HKEY_LOCAL_MACHINE",
                "SOFTWARE\\Microsoft\\Windows NT\\CurrentVersion",
                key
            )

        osName = get('ProductName')
        build = get('CurrentBuildNumber')

        version: str = '{} (build {}) {} (Py{})'.format(
            osName, build, bit, platform.python_version())
        return version
    except Exception as ex:
        print('获取系统版本失败，错误：' + str(ex))
        return '未知系统版本.'


def GetSystemVersionUnix() -> str:
    '''
    获取系统版本（unix）
    Returns
    -------
    str
        系统版本.
    '''
    try:
        version: str = readFile('/etc/redhat-release')
        if not version:
            version = readFile(
                '/etc/issue'
            ).strip().split("\n")[0].replace('\\n','').replace('\l','').strip()
        else:
            version = version.replace(
                'release ',''
            ).replace('Linux','').replace('(Core)','').strip()
        v = sys.version_info
        return version + '(Py {}.{}.{})'.format(v.major, v.minor, v.micro)
    except Exception as err:
        print('获取系统版本失败，错误：', err)
        return '未知系统版本.'


def GetBootTime() -> dict:
    '''
    获取当前系统启动时间
    Returns
    -------
    dict
        DESCRIPTION.
    '''
    bootTime: float = psutil.boot_time()
    return {
        'timestamp': bootTime,
        'runtime': time.time() - bootTime,
        'datetime': time.strftime('%Y-%m-%d %H:%M:%S', time.localtime())
    }


def GetCpuConstants() -> dict:
    '''
    获取CPU常量信息
    Parameters
    ----------
    cpuConstants : CpuConstants
        DESCRIPTION.
    Returns
    -------
    dict
        DESCRIPTION.
    '''
    return cpuConstants.getDict


def GetFullSystemData() -> dict:
    '''
    获取完全的系统信息
    Returns
    -------
    dict
        DESCRIPTION.
    '''
    systemData: dict = {
        **GetSystemInfo(),
        'network': { **GetNetWork() },
        'io': { **GetIoReadWrite() },
        'boot': { **GetBootTime() },
        'time': time.time()
    }
    return systemData

cpuConstants = CpuConstants()

if __name__ == '__main__':
    print(GetFullSystemData())
    print(GetCpuConstants())
    print(GetSystemInfo())
    print(GetNetWork())
    print(GetIoReadWrite())
```
