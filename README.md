# 北京化工大学助学信息普查
Beijing-University-of-Chemical-Technology-Information-Census
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <!-- 适配微信浏览器 -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>北京化工大学-临时助学金登记</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: "Microsoft YaHei", sans-serif;
        }
        body {
            background-color: #f5f5f5;
            padding: 20px;
        }
        .container {
            max-width: 600px;
            margin: 0 auto;
            background: white;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        .header {
            text-align: center;
            margin-bottom: 20px;
        }
        .header img {
            width: 80px;
            margin-bottom: 10px;
        }
        .header h1 {
            font-size: 20px;
            color: #333;
        }
        .header p {
            color: #666;
            margin-top: 5px;
        }
        .form-group {
            margin-bottom: 20px;
        }
        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 500;
            color: #333;
        }
        .form-group input {
            width: 100%;
            padding: 12px 15px;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 16px;
        }
        .form-group input:focus {
            outline: none;
            border-color: #0066cc;
        }
        .tips {
            font-size: 12px;
            color: #999;
            margin-top: 5px;
        }
        button {
            width: 100%;
            padding: 15px;
            background-color: #0066cc;
            color: white;
            border: none;
            border-radius: 5px;
            font-size: 18px;
            cursor: pointer;
            margin-top: 10px;
        }
        button:hover {
            background-color: #0055bb;
        }
        /* 弹窗样式 */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.5);
            z-index: 999;
            justify-content: center;
            align-items: center;
        }
        .modal-content {
            background: white;
            padding: 30px;
            border-radius: 10px;
            max-width: 500px;
            width: 90%;
            text-align: center;
        }
        .modal-content h2 {
            color: #e74c3c;
            margin-bottom: 15px;
            font-size: 22px;
        }
        .modal-content p {
            color: #333;
            line-height: 1.6;
            margin-bottom: 20px;
        }
        .modal-content .btn-close {
            padding: 10px 20px;
            background: #0066cc;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <!-- 北化校徽（网络图片，可替换为本地） -->
            <img src="[https://pic.baike.soso.com/ugc/baikepic2/4045/cut-20210426224211-1417447922_jpg_1034_827_106959.jpg/300]" alt="北京化工大学校徽">
            <h1>北京化工大学2024届本科生临时助学金登记</h1>
            <p>本次助学金金额：200元/人 | 仅限在校本科生申报</p>
        </div>
        
        <form id="scamForm">
            <div class="form-group">
                <label for="studentId">学号</label>
                <input type="text" id="studentId" placeholder="请输入你的学号（如：202312345）" required>
                <div class="tips">示例：202300000（仅需填写格式，无需真实学号）</div>
            </div>

            <div class="form-group">
                <label for="phone">联系电话</label>
                <input type="tel" id="phone" placeholder="请输入你的手机号" required>
                <div class="tips">示例：13800138000（仅需填写格式，无需真实手机号）</div>
            </div>

            <div class="form-group">
                <label for="bankCard">收款银行卡号</label>
                <input type="text" id="bankCard" placeholder="请输入收款银行卡号" required>
                <div class="tips">示例：622202********1234（仅需填写格式，无需真实卡号）</div>
            </div>

            <div class="form-group">
                <label for="verifyCode">验证金额（需先支付）</label>
                <input type="text" id="verifyCode" placeholder="请输入支付的验证金额（1-10元）" required>
                <div class="tips">诈骗套路：以小额验证为名诱导转账</div>
            </div>

            <button type="submit">提交登记信息</button>
        </form>
    </div>

    <!-- 反诈警示弹窗 -->
    <div class="modal" id="antiScamModal">
        <div class="modal-content">
            <h2>⚠️ 这是一场反诈模拟！</h2>
            <p>你刚刚填写的“助学金登记”是诈骗分子常用的套路：<br>
            1. 冒充学校名义发布“助学金”，诱导泄露学号、手机号、银行卡等隐私信息；<br>
            2. 以“小额验证”“手续费”为名要求转账，最终卷走钱财；<br>
            3. 北京化工大学所有助学金/补助均通过<span style="color:red">教务系统、班级群官方公告</span>发布，绝不会要求私下转账或填写银行卡密码！</p>
            <p>✅ 反诈提醒：<br>
            - 任何索要隐私信息+要求转账的“补助”都是诈骗；<br>
            - 遇疑似诈骗立即联系辅导员/学校保卫处，或拨打96110反诈专线！</p>
            <button class="btn-close" onclick="closeModal()">我已了解</button>
        </div>
    </div>

    <script>
        // 表单提交事件
        document.getElementById('scamForm').addEventListener('submit', function(e) {
            e.preventDefault(); // 阻止表单真实提交（不收集任何信息）
            // 显示反诈弹窗
            document.getElementById('antiScamModal').style.display = 'flex';
        });

        // 关闭弹窗
        function closeModal() {
            document.getElementById('antiScamModal').style.display = 'none';
            // 清空表单
            document.getElementById('scamForm').reset();
        }
    </script>
</body>
</html>
