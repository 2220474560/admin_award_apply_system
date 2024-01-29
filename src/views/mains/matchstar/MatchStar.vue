<!--
    * @FileDescription: 竞赛之星页面。
    * @Author: 李雪茹
    * @Date: 2024年1月22日
    * @LastEditors: 李思佳
    * @LastEditTime: 2024年1月22日
-->
<template>
  <div class="top">
    <a-input-search v-model:value="inputValue" placeholder="请输入内容" style="width: 200px" @search="onSearch" />
    <a-dropdown class="right">
      <template #overlay>
        <a-menu @click="handleMenuClick">
          <a-menu-item key="1"> 名单 </a-menu-item>
          <a-menu-item key="2"> 证书 </a-menu-item>
        </a-menu>
      </template>
      <a-button>
        导出竞赛之星
        <DownOutlined />
      </a-button>
    </a-dropdown>
  </div>
  <a-table :columns="columns" :data-source="filteredData" :pagination="false" class="responsive-table" bordered>
    <template #bodyCell="{column, record}">
      <template v-if="column.dataIndex === 'materials'">
        <a>{{ record.materials }}</a>
      </template>
      <template v-else-if="column.dataIndex === 'state'">
        <a v-for="tag in record.state" :key="tag" :style="{color: tag === '已通过' ? 'green' : tag === '未通过' ? 'red' : 'black'}">{{ tag }}</a>
      </template>
      <template v-else-if="column.dataIndex === 'operate'">
        <span>
          <template v-for="action in record.operate" :key="action">
            <a v-if="action === '查看证书' || action === '查看驳回理由'" :style="{color: action === '查看证书' ? 'green' : 'red'}">
              {{ action }}
            </a>
            <a-tag v-else :color="action === '通过' ? 'green' : 'red'">
              {{ action }}
            </a-tag>
          </template>
        </span>
      </template>
    </template>
  </a-table>
</template>

<script setup lang="ts">
import {ref} from 'vue';
import {DownOutlined} from '@ant-design/icons-vue';
import type {MenuProps} from 'ant-design-vue';
const inputValue = ref<string>('');
type DataType = {
  grade: string;
  major: string;
  class: string;
  name: string;
  cname: string;
  time: string;
  materials: string;
  state: string[];
  operate: string[];
};
const columns = [
  {
    title: '年级',
    dataIndex: 'grade',
    key: 'grade'
  },
  {
    title: '专业',
    dataIndex: 'major',
    key: 'major'
  },
  {
    title: '班级',
    dataIndex: 'class',
    key: 'class'
  },
  {
    title: '姓名',
    dataIndex: 'name',
    key: 'name'
  },
  {
    title: '竞赛名称',
    dataIndex: 'cname',
    key: 'cname'
  },
  {
    title: '报名时间',
    dataIndex: 'time',
    key: 'time'
  },
  {
    title: '佐证材料',
    dataIndex: 'materials',
    key: 'materials'
  },
  {
    title: '状态',
    dataIndex: 'state',
    key: 'state'
  },
  {
    title: '操作',
    dataIndex: 'operate',
    key: 'operate'
  }
];
const data = [
  {
    key: '1',
    grade: '2023级',
    major: '软件工程',
    class: '1',
    name: '李四',
    cname: '蓝桥杯',
    time: '2024/1/22',
    materials: '点击查看',
    state: ['未审批'],
    operate: ['通过', '未通过']
  },
  {
    key: '2',
    grade: '2023级',
    major: '软件工程',
    class: '1',
    name: '李四',
    cname: '蓝桥杯',
    time: '2024/1/22',
    materials: '点击查看',
    state: ['已通过'],
    operate: ['查看证书']
  },
  {
    key: '3',
    grade: '2023级',
    major: '软件工程',
    class: '1',
    name: '李四',
    cname: '蓝桥杯',
    time: '2024/1/22',
    materials: '点击查看',
    state: ['未通过'],
    operate: ['查看驳回理由']
  },
  {
    key: '4',
    grade: '2023级',
    major: '软件工程',
    class: '1',
    name: '李四',
    cname: '蓝桥杯',
    time: '2024/1/22',
    materials: '点击查看',
    state: ['未审批'],
    operate: ['查看驳回理由']
  }
];
const filteredData = ref<Array<DataType>>(data);
const onSearch = () => {
  filteredData.value = data.filter((item) => {
    const searchString = inputValue.value.toLocaleLowerCase();
    return item.major.includes(searchString) || item.name.includes(searchString) || item.cname.includes(searchString) || item.state.join(', ').includes(searchString);
  });
};
const handleMenuClick: MenuProps['onClick'] = (e) => {
  console.log('click', e);
};
</script>

<style scoped>
.top {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-bottom: 30px;
}
@media (min-width: 768px) {
  .top {
    flex-direction: row;
  }
}
@media (max-width: 768px) {
  .right {
    width: 200px;
    margin-top: 5px;
  }
  .responsive-table {
    max-width: 100%;
    overflow-x: auto;
  }
}
</style>
