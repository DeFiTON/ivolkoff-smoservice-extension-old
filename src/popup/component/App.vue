<template>
    <div v-if="aut == 'AUTH_LOAD'">
        <div class="text-center"><svg width='120px' height='120px' xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100" preserveAspectRatio="xMidYMid" class="uil-default"><rect x="0" y="0" width="100" height="100" fill="none" class="bk"></rect><rect  x='46.5' y='40' width='7' height='20' rx='5' ry='5' fill='#00b2ff' transform='rotate(0 50 50) translate(0 -30)'>  <animate attributeName='opacity' from='1' to='0' dur='1s' begin='0s' repeatCount='indefinite'/></rect><rect  x='46.5' y='40' width='7' height='20' rx='5' ry='5' fill='#00b2ff' transform='rotate(30 50 50) translate(0 -30)'>  <animate attributeName='opacity' from='1' to='0' dur='1s' begin='0.08333333333333333s' repeatCount='indefinite'/></rect><rect  x='46.5' y='40' width='7' height='20' rx='5' ry='5' fill='#00b2ff' transform='rotate(60 50 50) translate(0 -30)'>  <animate attributeName='opacity' from='1' to='0' dur='1s' begin='0.16666666666666666s' repeatCount='indefinite'/></rect><rect  x='46.5' y='40' width='7' height='20' rx='5' ry='5' fill='#00b2ff' transform='rotate(90 50 50) translate(0 -30)'>  <animate attributeName='opacity' from='1' to='0' dur='1s' begin='0.25s' repeatCount='indefinite'/></rect><rect  x='46.5' y='40' width='7' height='20' rx='5' ry='5' fill='#00b2ff' transform='rotate(120 50 50) translate(0 -30)'>  <animate attributeName='opacity' from='1' to='0' dur='1s' begin='0.3333333333333333s' repeatCount='indefinite'/></rect><rect  x='46.5' y='40' width='7' height='20' rx='5' ry='5' fill='#00b2ff' transform='rotate(150 50 50) translate(0 -30)'>  <animate attributeName='opacity' from='1' to='0' dur='1s' begin='0.4166666666666667s' repeatCount='indefinite'/></rect><rect  x='46.5' y='40' width='7' height='20' rx='5' ry='5' fill='#00b2ff' transform='rotate(180 50 50) translate(0 -30)'>  <animate attributeName='opacity' from='1' to='0' dur='1s' begin='0.5s' repeatCount='indefinite'/></rect><rect  x='46.5' y='40' width='7' height='20' rx='5' ry='5' fill='#00b2ff' transform='rotate(210 50 50) translate(0 -30)'>  <animate attributeName='opacity' from='1' to='0' dur='1s' begin='0.5833333333333334s' repeatCount='indefinite'/></rect><rect  x='46.5' y='40' width='7' height='20' rx='5' ry='5' fill='#00b2ff' transform='rotate(240 50 50) translate(0 -30)'>  <animate attributeName='opacity' from='1' to='0' dur='1s' begin='0.6666666666666666s' repeatCount='indefinite'/></rect><rect  x='46.5' y='40' width='7' height='20' rx='5' ry='5' fill='#00b2ff' transform='rotate(270 50 50) translate(0 -30)'>  <animate attributeName='opacity' from='1' to='0' dur='1s' begin='0.75s' repeatCount='indefinite'/></rect><rect  x='46.5' y='40' width='7' height='20' rx='5' ry='5' fill='#00b2ff' transform='rotate(300 50 50) translate(0 -30)'>  <animate attributeName='opacity' from='1' to='0' dur='1s' begin='0.8333333333333334s' repeatCount='indefinite'/></rect><rect  x='46.5' y='40' width='7' height='20' rx='5' ry='5' fill='#00b2ff' transform='rotate(330 50 50) translate(0 -30)'>  <animate attributeName='opacity' from='1' to='0' dur='1s' begin='0.9166666666666666s' repeatCount='indefinite'/></rect></svg></div>
    </div>
    <div v-else-if="aut == 'AUTH_SUCCESS'">
        <div class="row filter">
            <div class="pull-left">
                <div class="status">Со статусом:
                    <select id="status-filter" v-model="statusFilter" v-on:change="filterStatusFilter">
                        <option value="">- Любой статус -</option>
                        <option value="0">Новый</option>
                        <option value="1">Оплачивается</option>
                        <option value="2">Оплачен</option>
                        <option value="3">Выполняется</option>
                        <option value="4">Принят системой</option>
                        <option value="5">Завершен2</option>
                        <option value="7">В очереди</option>
                        <option value="8">Завершён</option>
                        <option value="9">Отменён</option>
                    </select></div>
            </div>
            <div class="pull-right text-right">
                <div class="num_order">
                    <input type="text" size="10" placeholder="№ заказа" id="invoice-search-id" v-model="invoiceSearchId">
                    <input type="button" value="Найти" id="invoice-search-button" v-on:click="filterSearchId">
                    <input type="button" value="Сброс поиска" id="invoice-search-reset" v-on:click="filterReset">
                </div>
            </div>
        </div>
        <table width="100%" cellspacing="1" cellpadding="0" border="0" bgcolor="#ffffff" class="gTable table" id="invoice-table" v-html="invoiceTable"></table>
        <div id="paginator" class="paginator text-center">
            <span v-for="i in paginator.all">
                <span class="pgSwchA" v-if="(i == paginator.current)"><b>{{ i }}</b></span>
                <a href="#" class="pgSwch" v-on:click="filterPage(i)" v-if="(i != paginator.current)"><span>{{ i }}</span></a>
            </span>
        </div>
        <div class="paginator text-center sublink">
            <a href="https://smoservice.ru/index/8" target="_blank">Личный кабинет</a>
            <a href="https://smoservice.ru/news" target="_blank">Новости</a>
            <a href="https://smoservice.ru/faq" target="_blank">FAQ</a>
            <a href="http://support.smoservice.ru" target="_blank">Служба поддержка</a>
        </div>
    </div>
    <div v-else-if="aut == 'AUTH_FAIL'">
        <div class="text-center">
            <div class="col-xs-6 col-xs-offset-3">
                <a class="zakazat" v-bind:href="BASE_DOMAIN + 'index/1'" style="margin-top: 46px;" target="_blank">Авторизоваться</a>
            </div>
        </div>
    </div>
    <div v-else>
        Не понятно
    </div>
</template>

<script type="text/babel">
    import 'bootstrap';
    import './../../asset/css/my.css';
    import './../../asset/css/style.css';

    import {BASE_DOMAIN, AUTH_LOAD, AUTH_SUCCESS, AUTH_FAIL} from './../constant.js';

    console.info('BASE_DOMAIN = ', BASE_DOMAIN);

    export default {
        data() {
            setTimeout(() => {
                this.checkAuth();
            }, 1000);
            return {
                BASE_DOMAIN: BASE_DOMAIN,
                aut: AUTH_LOAD,
                invoiceSearchId: '',
                statusFilter: '',
                invoiceTable: '',
                paginator: {
                    all: 5,
                    current: 1
                },
                ssid: null,
            };
        },
        methods: {
            checkAuth: function () {
                $.ajax({
                    url: BASE_DOMAIN + 'shop/invoices',
                    dataType: 'html',
                    type: 'get'
                }).done((data) => {
                    //console.info('checkAuth.done | data = ', data);
                    var s = data.indexOf('Доступ запрещен');
                    console.info('checkAuth.done | s = ', s);
                    if (s == -1) {
                        this.aut = AUTH_SUCCESS;
                        this.drawOrder(data);
                    } else {
                        this.aut = AUTH_FAIL;
                    }
                }).fail((jqXHR, textStatus, errorThrown) => {
                    console.info('checkAuth.fail | jqXHR = ', jqXHR);
                    console.info('checkAuth.fail | textStatus = ', textStatus);
                    this.aut = AUTH_FAIL;
                });
            },
            drawOrder: function (data) {
                this.ssid = data.match(/var ssid = '(.*?)';/)[1];
                console.info('drawOrder | ssid = ', this.ssid);

                data = $(data);

                var invoiceTable = this.invoiceTableReDraw(data.find("#invoice-table")).html();
                console.info('drawOrder | invoiceTable = ', invoiceTable);
                this.invoiceTable = invoiceTable;
                console.info('drawOrder | this.invoiceTable = ', invoiceTable);

                if (data.find('.pgSwch').length) {
                    var paginator = data.find('.pgSwch').parent();
                    console.info('drawOrder | paginator = ', paginator);
                    this.paginator = {
                        all: Math.max(parseInt(paginator.find('a').last().text()), parseInt(paginator.find('b').text())),
                        current: parseInt(paginator.find('b').text())
                    };
                } else {
                    this.paginator = {
                        all: 0,
                        current: 0
                    };
                }
            },
            drawOrderAjax: function (data) {
                var invoiceTable = $('<p/>').append($(data).find('cmd[t="invoice_cont"]').text());
                invoiceTable = this.invoiceTableReDraw(invoiceTable.find("#invoice-table")).html();
                //console.info('drawOrder | this.invoiceTable = ', this.invoiceTable);
                this.invoiceTable = invoiceTable;

                var paginator = $('<p/>').append($(data).find('cmd[t="plist"]').text());
                if (paginator.find('b').length) {
                    console.info('drawOrder | paginator = ', paginator.html());
                    paginator = {
                        all: Math.max(parseInt(paginator.find('a').last().text()), parseInt(paginator.find('b').text())),
                        current: parseInt(paginator.find('b').text())
                    };
                    console.info('drawOrder | paginator = ', paginator);
                    this.paginator = paginator;
                } else {
                    this.paginator = {
                        all: 0,
                        current: 0
                    };
                }
            },
            filterSearchId: function () {
                this.makeFilterOrder({
                    filter: [
                        {
                            name: 'id',
                            id: this.invoiceSearchId
                        }
                    ]
                });
            },
            filterStatusFilter: function () {
                this.makeFilterOrder({
                    filter: [
                        {
                            name: 'id',
                            id: ''
                        }, {
                            name: 'status',
                            id: this.statusFilter
                        }
                    ]
                });
            },
            filterPage: function (page) {
                this.makeFilterOrder({
                    filter: [
                        {
                            name: 'page',
                            id: page
                        }
                    ]
                });
            },
            filterReset: function () {
                this.makeFilterOrder({
                    filter: [
                        {
                            name: 'status',
                            id: ''
                        }, {
                            name: 'page',
                            id: '1'
                        }, {
                            name: 'id',
                            id: '№ заказа'
                        }
                    ]
                });
            },
            makeFilterOrder: function (param) {
                param = $.extend({}, {
                    filter: [
                        {
                            name: 'status',
                            id: ''
                        }
                    ]
                }, param);

                console.info('makeFilterOrder | param = ', param);

                $.each(param.filter, function (i, filter) {
                    console.info('makeFilterOrder | i = ', i, ' | filter = ', filter);
                    $.ajax({
                        url: BASE_DOMAIN + 'shop/invoices',
                        async: false,
                        data: {
                            filter: filter.name,
                            id: filter.id,
                            ssid: this.ssid,
                            _tp_: 'xml'
                        },
                        dataType: 'xml',
                        type: 'post'
                    });
                });

                console.info('makeFilterOrder | param.filter = ', param.filter);
                var paramFilterLast = param.filter.splice(-1)[0];
                console.info('makeFilterOrder | paramFilterLast = ', paramFilterLast);

                $.ajax({
                    url: BASE_DOMAIN + 'shop/invoices',
                    data: {
                        filter: paramFilterLast.name,
                        id: paramFilterLast.id,
                        ssid: this.ssid,
                        _tp_: 'xml'
                    },
                    dataType: 'xml',
                    type: 'post',
                }).done((data) => {
                    console.info('makeFilterOrder | data = ', data);

                    var s = $(data).find('ajax').html().indexOf('Доступ запрещен');
                    console.info('checkAuth.done | s = ', s);
                    if (s == -1) {
                        this.aut = AUTH_SUCCESS;
                        this.drawOrderAjax(data);
                    } else {
                        this.aut = AUTH_FAIL;
                    }
                }).fail((jqXHR, textStatus, errorThrown) => {
                    console.info('function filter_order().ajax.error | jqXHR = ', jqXHR);
                    console.info('function filter_order().ajax.error | textStatus = ', textStatus);
                    this.aut = AUTH_FAIL;
                });
            },
            invoiceTableReDraw: function (invoiceTable) {
                invoiceTable.find('tr:nth-child(1) td:nth-child(1)').html('№');
                invoiceTable.find('tr').each(function () {
                    $(this).find('td:nth-child(1) small').remove();
                    //Все что после сслки
                    $(this).find('td:nth-child(n + 4)').remove();
                });
                invoiceTable.find('a').each(function () {
                    var t = $(this).text();
                    $(this).replaceWith(t);
                });
                invoiceTable.find('[onclick]').attr('onclick', '');
                invoiceTable.find('[title]').attr('title', '');

                console.info('invoiceTable = ', invoiceTable);
                return invoiceTable;
            }
        },
        components: {}
    }
</script>