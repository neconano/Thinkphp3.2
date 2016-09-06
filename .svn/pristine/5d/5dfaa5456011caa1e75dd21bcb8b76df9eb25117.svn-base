<?php
// +----------------------------------------------------------------------
// | ThinkPHP [ WE CAN DO IT JUST THINK IT ]
// +----------------------------------------------------------------------
// | Copyright (c) 2006-2013 http://thinkphp.cn All rights reserved.
// +----------------------------------------------------------------------
// | Licensed ( http://www.apache.org/licenses/LICENSE-2.0 )
// +----------------------------------------------------------------------
// | Author: 麦当苗儿 <zuojiazi@vip.qq.com> <http://www.zjzit.cn>
// +----------------------------------------------------------------------
namespace Think;

class AjaxPageTo {
    // 分页栏每页显示的页数
    public $rollPage = 5;
    // 页数跳转时要带的参数
    public $parameter  ;
    // 默认列表每页显示行数
    public $listRows = 20;
    // 起始行数
    public $firstRow ;
    // 分页总页面数
    protected $totalPages  ;
    // 总行数
    protected $totalRows  ;
    // 当前页数
    protected $nowPage    ;
    // 分页的栏的总页数
    protected $coolPages   ;
    // 分页显示定制
    protected $config  = array('prev'=>'<li><</li>','next'=>'<li class="mr00">></li>','first'=>'第一页','last'=>'最后一页','theme'=>'<ul> %upPage% %linkPage% %downPage% </ul>');
    // 默认分页变量名
    protected $varPage;


    public function __construct($totalRows,$listRows,$now_page = 1,$ajax_func=array()) {
        $this->totalRows = $totalRows;
        $this->ajax_func = $ajax_func;
        if(!empty($listRows)) {
            $this->listRows = intval($listRows);
        }
        if(!empty($now_page)) {
            $this->nowPage = intval($now_page);
        }
        $this->totalPages = ceil($this->totalRows/$this->listRows);     //总页数
        $this->coolPages  = ceil($this->totalPages/$this->rollPage);
        if(!empty($this->totalPages) && $this->nowPage>$this->totalPages) {
            $this->nowPage = $this->totalPages;
        }
        $this->firstRow = $this->listRows*($this->nowPage-1);
    }

public function setConfig($name,$value) {
        if(isset($this->config[$name])) {
            $this->config[$name]    =   $value;
        }
    }


    public function show() {
        if(0 == $this->totalRows) return '';
        $nowCoolPage      = ceil($this->nowPage/$this->rollPage);

        //上下翻页字符串
        $upRow   = $this->nowPage-1;
        $downRow = $this->nowPage+1;
        if ($upRow>0){
            $upPage='<a href=javascript:'.$this->ajax_func['paramfun'].'('.$this->ajax_func['param1'].','.$this->ajax_func['param2'].','.$this->ajax_func['param3'].','.$upRow.')>'.$this->config['prev'].'</a>';
        }else{
            $upPage="";
        }

if ($downRow <= $this->totalPages){
            $downPage='<a href=javascript:'.$this->ajax_func['paramfun'].'('.$this->ajax_func['param1'].','.$this->ajax_func['param2'].','.$this->ajax_func['param3'].','.$downRow.')>'.$this->config['next'].'</a>';
        }else{
            $downPage="";
        }
        // << < > >>
        if($nowCoolPage == 1){
            $theFirst = "";
            $prePage = "";
        }else{
            $preRow =  $this->nowPage-$this->rollPage;
            $prePage = '<a href=javascript:'.$this->ajax_func['paramfun'].'('.$this->ajax_func['param1'].','.$this->ajax_func['param2'].','.$this->ajax_func['param3'].','.$preRow.')>上'.$this->rollPage.'页</a>';
            $theFirst = '<a href=javascript:'.$this->ajax_func['paramfun'].'('.$this->ajax_func['param1'].','.$this->ajax_func['param2'].','.$this->ajax_func['param3'].',1)>'.$this->config['first'].'</a>';
        }
        if($nowCoolPage == $this->coolPages){
            $nextPage = "";
            $theEnd="";
        }else{
            $nextRow = $this->nowPage+$this->rollPage;
            $theEndRow = $this->totalPages;
            $nextPage = '<a href=javascript:'.$this->ajax_func['paramfun'].'('.$this->ajax_func['param1'].','.$this->ajax_func['param2'].','.$this->ajax_func['param3'].','.$nextRow.')>下'.$this->rollPage.'页</a>';
            $theEnd = '<a href=javascript:'.$this->ajax_func['paramfun'].'('.$this->ajax_func['param1'].','.$this->ajax_func['param2'].','.$this->ajax_func['param3'].','.$theEndRow.')>'.$this->config['last'].'</a>';
        }
        // 1 2 3 4 5
        $linkPage = "";
        for($i=1;$i<=$this->rollPage;$i++){
            $page=($nowCoolPage-1)*$this->rollPage+$i;
            if($page!=$this->nowPage){
                if($page<=$this->totalPages){
                   $linkPage .= '<li><a href=javascript:'.$this->ajax_func['paramfun'].'('.$this->ajax_func['param1'].','.$this->ajax_func['param2'].','.$this->ajax_func['param3'].','.$page.')>&nbsp;'.$page.'&nbsp;</a></li>';
                }else{
                    break;
                }
            }else{
                if($this->totalPages != 1){
                    $linkPage .= '<li class="page_v422_current">'.$page.'</li>';
                }
            }
        }
        $linkPage.='';
        $pageStr  =  str_replace(
            array('%upPage%','%downPage%','%linkPage%'),
            array($upPage,$downPage,$linkPage),$this->config['theme']);
        return $pageStr;
    }

}
