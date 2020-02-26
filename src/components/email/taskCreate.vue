<template>
    <div class="taskCreateLayout">
        <div class="left-content">
            <div class="steps">
                <a-steps direction="vertical" size="small">
                    <a-step title="基本信息" :status="steps1.one"/>
                    <a-step title="邮件列表" :status="steps1.two"/>
                    <a-step title="回复邮箱" :status="steps1.three"/>
                    <a-step title="邮件标题" :status="steps1.four"/>
                    <a-step title="邮件内容" :status="steps1.five"/>
                    <a-step title="完成"/>
                </a-steps>
            </div>
        </div>
        <div class="content-body">
            <div class="config-content" v-if="showOne">
                <div class="content-item">
                    <div class="infos">
                        <p class="item-title">项目名称</p>
                        <a-input size="large" v-model="project.name"></a-input>
                    </div>
                    <div class="infos">
                        <p class="item-title">项目进度 (%)</p>
                        <a-input-number
                                size="large"
                                :min="0"
                                :max="100"
                                v-model="project.schedule"></a-input-number>
                    </div>
                </div>
                <div class="content-item">
                    <div class="infos">
                        <p class="item-title">项目简介</p>
                        <a-input type="textarea" :rows="3" size="large" placeholder="介绍一下这个项目"
                                 v-model="project.description"></a-input>
                    </div>
                </div>
                <div class="content-item">
                    <div class="infos">
                        <p class="item-title">项目公开性</p>
                        <a-select
                                size="large"
                                v-model="project.private"
                        >
                            <a-select-option :key="0">
                                公开项目（所有人都可通过链接访问，仅项目成员可编辑）
                            </a-select-option>
                            <a-select-option :key="1">
                                私有项目（仅项目成员可查看和编辑）
                            </a-select-option>
                        </a-select>
                    </div>
                </div>
                <div class="content-item">
                    <div class="infos">
                        <p class="item-title">项目拥有者</p>
                        <div class="m-t">
                            <a-avatar :src="project.owner_avatar"></a-avatar>
                            <span class="m-l">{{project.owner_name}}</span>
                            <!--<a-button class="middle-btn pull-right" size="large">
                                移交
                            </a-button>-->
                        </div>
                    </div>
                </div>
                <a-divider/>
                <div class="content-item">
                    <div class="infos">
                        <div class="btns">
                            <a-button type="primary" class="middle-btn pull-right" size="large"
                                      @click="saveProject">
                                下一步
                            </a-button>
                        </div>
                    </div>
                </div>
            </div>
            <div class="config-content" v-if="showTwo">
                <div class="content-item">
                    <div class="infos">
                        <p class="item-title">项目名称</p>
                        <a-input size="large" v-model="project1.name"></a-input>
                    </div>
                    <div class="infos">
                        <p class="item-title">项目进度 (%)</p>
                        <a-input-number
                                size="large"
                                :min="0"
                                :max="100"
                                v-model="project1.schedule"></a-input-number>
                    </div>
                </div>
                <div class="content-item">
                    <div class="infos">
                        <p class="item-title">项目简介</p>
                        <a-input type="textarea" :rows="3" size="large" placeholder="介绍一下这个项目"
                                 v-model="project1.description"></a-input>
                    </div>
                </div>
                <div class="content-item">
                    <div class="infos">
                        <p class="item-title">项目公开性</p>
                        <a-select
                                size="large"
                                v-model="project1.private"
                        >
                            <a-select-option :key="0">
                                公开项目（所有人都可通过链接访问，仅项目成员可编辑）
                            </a-select-option>
                            <a-select-option :key="1">
                                私有项目（仅项目成员可查看和编辑）
                            </a-select-option>
                        </a-select>
                    </div>
                </div>
                <div class="content-item">
                    <div class="infos">
                        <p class="item-title">项目拥有者</p>
                        <div class="m-t">
                            <a-avatar :src="project1.owner_avatar"></a-avatar>
                            <span class="m-l">{{project1.owner_name}}</span>
                            <!--<a-button class="middle-btn pull-right" size="large">
                                移交
                            </a-button>-->
                        </div>
                    </div>
                </div>
                <a-divider/>
                <div class="content-item">
                    <div class="infos" style="">
                        <div class="btns">
                            <a-button type="primary" class="middle-btn pull-right" size="large"
                                      @click="saveProject1">
                                上一步
                            </a-button>
                            <div style="margin-left: 15px">
                                <a-button type="primary" class="middle-btn pull-right" size="large"
                                                @click="saveProject1">
                                    下一步
                                </a-button>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import {notice} from "../../assets/js/notice";
    import {checkResponse, getApiUrl, getAuthorization, getBase64} from "../../assets/js/utils";

    export default {
        name: "taskCreate",
        props: {
            code: {
                type: [String],
                default() {
                    return ''
                }
            },
        },
        data() {
            return {
                /*项目设置*/
                loading: false,
                project: {},
                project1: {},
                showOne: true,
                showTwo: false,
                steps1:{
                    one: "process",
                    two: "wait",
                    three: "wait",
                    four: "wait",
                    five: "wait"
                }
            }
        },
        computed: {
            headers() {
                return getAuthorization();
            }
        },
        methods: {
            saveProject() {
                this.showOne = false;
                this.showTwo = true;
                this.steps1.one = "finish";
                this.steps1.two = "process";
            },

            saveProject1() {
                this.showOne = true;
                this.showTwo = false;
            }
        }
    }
</script>

<style lang="less">
    .taskCreateLayout{
        display: flex;
        justify-content: left;

        .ant-modal-body {
            padding: 0;
        }

        .ant-modal-body, .ant-tabs, .ant-tabs-bar {
            min-width: 180px;

            .ant-tabs-tab {
                padding: 12px 24px;
            }
        }

        .left-content{
            border-right: 1px solid #e8e8e8;
            min-width: 180px;
            .steps{
                margin-left: 20px;
                margin-right: 10px;
                margin-top: 20px;
            }
        }
        .content-body{
            .config-content {
                padding-left: 24px;
                padding-right: 24px;
                padding-top: 18px;
                min-width: 620px;
                min-height: 520px;
                .content-item {
                    display: flex;
                    justify-content: space-between;
                    flex: 1 1;
                    margin-bottom: 24px;

                    .infos {
                        width: 100%;
                        padding-right: 12px;

                        p {
                            margin-bottom: 6px;
                        }

                        .item-title {
                            font-size: 16px;
                        }

                        .item-tips {
                            margin-bottom: 12px;
                        }

                        .ant-select {
                            width: 100%;
                        }

                        .ant-input-number-lg {
                            width: 100%;
                        }

                        .cover-item {
                            display: flex;

                            img {
                                width: 300px;
                                height: 150px;
                            }

                            .cover-uploader {
                                display: block;
                                margin-left: 24px;

                                .upload-tips {
                                    margin-top: 12px;
                                }
                            }
                        }
                        .btns{
                            position: relative;
                            display: flex;
                            justify-content: center;
                        }
                    }
                }

                &.task-config {
                    .content-item {
                        padding-bottom: 24px;
                        padding-right: 16px;
                        border-bottom: 1px solid #e5e5e5;
                    }

                    .prefix-input {
                        width: 50%;
                        margin-right: 24px;
                    }
                }

                .task-workflow {
                    .workflow-content {
                        margin-top: 12px;

                        .workflow-rule-item {
                            margin-bottom: 16px;

                            p {
                                color: rgba(0, 0, 0, 0.45);
                            }
                        }
                    }
                }

                &.more-config {
                    .ant-btn {
                        margin-right: 12px;
                    }
                }
            }
        }
    }
</style>
