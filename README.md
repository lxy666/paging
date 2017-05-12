# paging
分页
js实现分页效果
goPage(1,15);//指的是当前页为第一页，15条数据为一页
然后计算出一共分为几页

       var totalPage = 0;//总页数
        var pageSize = psize;//每页显示行数
        if (num / pageSize > parseInt(num / pageSize)) {//假设有20条数据，15条数据页 
            totalPage = parseInt(num / pageSize) + 1;//1.333>1 ,所以分为两页
        } else {
            totalPage = parseInt(num / pageSize);//若有45条数据，则分为3页
        }
计算开始显示的行数，和最后显示的行数

       var currentPage = pno;//当前页数
        var startRow = (currentPage - 1) * pageSize + 1;//开始显示的行  1
        var endRow = currentPage * pageSize;//结束显示的行   15
        endRow = (endRow > num) ? num : endRow;
遍历显示数据实现分页

 for (var i = 1; i < (num + 1); i++) {
            var irow = itable.rows[i - 1];
            if (i >= startRow && i <= endRow) {
                irow.style.display = "block";//当前页的数据
            } else {
                irow.style.display = "none";//非当前页的数据
            }
        }
实现最下方的显示，第几页，上一页，下一页
当前页为第一页时，上一页没有点击事件
当前页为最后一页时，下一页没有点击事件
否则，上一页和下一页均可使用，点击某一页会跳转到那一页

 if (currentPage > 1) {
            tempStr += "<a href=\"#\" onClick=\"goPage(" + (currentPage - 1) + "," + psize + ")\"><上一页&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</a>"
            for (var j = 1; j <= totalPage; j++) {
                tempStr += "<a href=\"#\" onClick=\"goPage(" + j + "," + psize + ")\">" + j + "&nbsp;&nbsp;&nbsp;</a>"
            }
        } else {
            tempStr += "<上一页&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;";
            for (var j = 1; j <= totalPage; j++) {
                tempStr += "<a href=\"#\" onClick=\"goPage(" + j + "," + psize + ")\">" + j + "&nbsp;&nbsp;&nbsp;</a>"
            }
        }
        if (currentPage < totalPage) {
            tempStr += "<a href=\"#\" onClick=\"goPage(" + (currentPage + 1) + "," + psize + ")\">下一页>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</a>";
            for (var j = 1; j <= totalPage; j++) {
            }
        } else {
            tempStr += "  下一页>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;";
            for (var j = 1; j <= totalPage; j++) {
            }
        }
