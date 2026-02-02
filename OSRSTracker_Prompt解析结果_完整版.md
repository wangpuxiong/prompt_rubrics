# Prompt解析结果

## 项目分析基础信息
- **项目名称**: OSRSTracker
- **技术栈**: Python/Flask/JavaScript/Plotly/Bootstrap 4
- **题目类型**: Code Creation | Code Modification
- **分析置信度**: 高

## 详细分析结果

### 技术栈
Python/Flask/JavaScript/Plotly/Bootstrap 4/pytest

**分析依据**:
- **从repo_summary提取**: Python、Flask、JavaScript、Plotly、Bootstrap 4、pytest
- **从prompt_text提取**: Python、OSRS API、Plotly
- **从项目结构推断**: 
  - 后端: Python/Flask (routing.py, backend/目录)
  - 前端: HTML/CSS/JavaScript (templates/目录)
  - 数据可视化: Plotly库
  - API集成: requests库 (player_info.py中使用)

### 题目类型
Code Creation | Code Modification

**判断依据**:
1. **Code Creation特征**:
   - "implement the item prices file" → 创建新文件
   - "create the 'item trends graph' script" → 创建新脚本
   - 全新的功能模块开发

2. **Code Modification特征**:
   - "Similar to how it was done in the player info Python file" → 参考现有实现模式
   - 需要遵循player_info.py的代码结构和风格
   - 与现有系统集成

3. **综合判断**: 这是一个创建新功能但需要参考现有代码模式的复合任务

### 显性需求列表
1. **创建物品价格文件**: 参考player_info.py的实现方式，创建item prices文件
2. **集成OSRS API**: 使用OSRS官方API获取物品价格数据
3. **创建图表生成脚本**: 创建"item trends graph"脚本
4. **使用Plotly生成图表**: 使用Plotly库生成价格趋势图表
5. **图表图片存储**: 将图表图片保存到包含所有物品趋势图表的文件夹中
6. **JSON数据分离存储**: 将物品价格的JSON文件保存到单独的文件夹中

### 隐性需求列表
1. **代码结构一致性** - 推断依据: prompt明确要求"Similar to how it was done in the player info Python file"，需要遵循player_info.py的代码架构模式（函数模块化、类型注解、错误处理等）

2. **API数据解析逻辑** - 推断依据: player_info.py中有parse_hiscores_data函数，新代码需要实现类似的parse_item_prices_data函数来处理OSRS物品价格API返回的数据格式

3. **文件夹自动创建** - 推断依据: player_info.py中使用os.makedirs('backend', exist_ok=True)确保目录存在，新代码需要为图表文件夹和数据文件夹实现类似的目录创建逻辑

4. **错误处理机制** - 推断依据: player_info.py中实现了完整的异常处理（requests.exceptions.RequestException、超时处理、状态码检查），新代码需要实现类似的健壮错误处理

5. **数据验证和清理** - 推断依据: player_info.py中有validate_username和sanitize_username函数，新代码可能需要类似的物品ID验证和数据清理逻辑

6. **文件命名规范** - 推断依据: player_info.py使用sanitize_username确保文件名安全，新代码需要制定合理的物品价格文件和图表文件命名规范

7. **代码风格统一** - 推断依据: player_info.py使用类型注解(Dict[str, Any], Optional)、详细的docstring、清晰的函数命名，新代码必须保持相同的代码风格

8. **边界情况处理** - 推断依据: player_info.py处理了-1值、空数据、API限流等情况，新代码需要处理无效物品ID、API限流、网络超时、数据格式异常等边界情况

9. **数据更新策略** - 推断依据: 项目是实时数据跟踪应用，需要考虑数据获取频率、缓存机制、避免重复API调用

10. **Flask应用集成** - 推断依据: routing.py中已有/economy路由但未实现，新功能需要与现有Flask路由系统集成，可能需要添加新的路由端点来展示物品价格和图表

11. **与现有模板兼容** - 推断依据: routing.py使用render_template渲染stats.html和economy.html，新功能可能需要更新economy.html模板来展示物品价格数据和图表

12. **性能优化考量** - 推断依据: 作为Web应用，需要考虑API调用效率、文件I/O性能、图表生成速度，避免阻塞Flask主线程

13. **可扩展性设计** - 推断依据: 项目计划开发经济模块，代码结构需要支持未来添加更多OSRS经济数据分析功能

14. **测试兼容性** - 推断依据: 项目使用pytest测试框架，新代码应该设计为可测试的，可能需要添加单元测试

### 约束条件列表
1. **技术栈约束** - 约束内容: 必须使用Python作为主要编程语言，必须使用Flask框架，必须使用Plotly库进行图表生成，必须使用OSRS官方API

2. **代码风格约束** - 约束内容: 必须遵循player_info.py的代码风格，包括使用类型注解、详细的docstring、清晰的函数命名（如get_item_prices、save_to_json等）

3. **架构设计约束** - 约束内容: 必须遵循backend/目录结构，新文件应创建在backend/目录下，必须保持与现有模块的分离和模块化设计

4. **第三方服务约束** - 约束内容: 必须使用OSRS官方API获取物品价格数据，不能使用其他数据源，需要处理API的限流和错误响应

5. **现有代码保护约束** - 约束内容: 不能修改或破坏现有的技能统计功能（player_info.py、stats.html、/路由），必须保持向后兼容

6. **文件组织约束** - 约束内容: 图表图片和JSON数据文件必须保存在不同文件夹中，不能混合存储，需要创建明确的文件夹结构（如backend/item_trend_graphs/和backend/item_prices_data/）

7. **参考模式约束** - 约束内容: 必须参考player_info.py的实现模式，包括API调用方式（requests.get with timeout）、数据解析函数结构、文件保存逻辑（save_to_json模式）、错误处理方式

8. **Flask集成约束** - 约束内容: 必须与现有Flask应用兼容，不能破坏现有路由，可能需要扩展/economy路由功能，需要与现有模板系统兼容

9. **数据格式约束** - 约束内容: JSON文件格式应该与现有skill_stats.json保持一致的风格（使用indent=4），确保数据可读性和一致性

10. **Docker兼容性约束** - 约束内容: 新功能必须支持Docker容器化部署，文件路径和目录结构需要考虑容器环境

11. **多语言支持约束** - 约束内容: 项目支持中英文双语界面，新功能如果需要用户界面，需要考虑国际化支持

12. **性能指标约束** - 约束内容: API调用应该有超时设置（参考player_info.py的timeout=10），避免长时间阻塞，图表生成应该高效，不影响Web应用响应速度

### Rubrics设计重点
基于题目类型 **Code Creation | Code Modification**，评估重点应包括：

1. **功能完整性**: 
   - 物品价格文件是否完全实现，包括API集成、数据解析、文件保存
   - 图表生成脚本是否完全实现，包括Plotly图表生成、图片保存
   - 文件夹结构是否正确分离图表和数据文件

2. **代码一致性**:
   - 新代码是否严格遵循player_info.py的结构模式（函数设计、命名规范、代码组织）
   - 错误处理逻辑是否与现有代码保持一致
   - 代码风格（类型注解、docstring、注释）是否统一

3. **API集成正确性**:
   - OSRS物品价格API的调用是否正确实现
   - 数据解析函数是否健壮可靠，能处理各种API响应格式
   - API错误处理是否完善（超时、限流、无效响应等）

4. **文件系统管理**:
   - 图表图片文件夹和数据文件夹是否正确分离
   - 文件命名和组织是否符合逻辑和规范
   - 文件夹创建逻辑是否健壮（使用os.makedirs with exist_ok=True）

5. **系统集成表现**:
   - 新功能是否与现有Flask应用无缝融合
   - 路由设计是否合理，不会与现有路由冲突
   - 模板集成是否平滑（如果需要更新economy.html）

6. **代码质量指标**:
   - 函数模块化程度是否合适（参考player_info.py的函数划分）
   - 代码注释和文档是否充分（docstring、类型注解）
   - 变量和函数命名是否清晰易懂

7. **边界情况处理**:
   - 对无效物品ID的处理
   - API限流和错误响应的处理
   - 文件系统异常的处理（权限、磁盘空间等）
   - 数据格式异常的处理

8. **可维护性评估**:
   - 代码结构是否易于后续扩展
   - 配置文件和硬编码值的管理
   - 日志和调试信息的设计

9. **性能考量**:
   - API调用的效率和缓存策略
   - 文件I/O操作的优化
   - 图表生成的性能（大文件、复杂图表）
   - 内存使用和资源管理

10. **参考模式遵循度**:
    - 是否真正参考了player_info.py的实现模式
    - API调用方式是否一致（requests.get、timeout设置）
    - 数据解析函数结构是否相似
    - 文件保存逻辑是否遵循相同模式

**关键成功指标**:
- ✅ 物品价格文件成功创建并正确使用OSRS API
- ✅ 图表生成脚本成功创建并使用Plotly生成趋势图
- ✅ 图表和数据文件正确分离到不同文件夹
- ✅ 代码风格与player_info.py高度一致
- ✅ 错误处理完善，能处理各种异常情况
- ✅ 与现有Flask应用无缝集成
- ✅ 代码结构清晰，易于维护和扩展

**潜在风险点**:
- ⚠️ **OSRS API端点未知**: 需要查找正确的物品价格API端点，可能需要研究OSRS API文档或使用第三方API包装库
  - 缓解建议: 先调研OSRS官方API文档，或使用python-osrsapi客户端库
  
- ⚠️ **API限流问题**: OSRS API可能有请求频率限制，频繁调用可能导致IP被封
  - 缓解建议: 实现请求频率控制、缓存机制、批量请求优化
  
- ⚠️ **图表文件格式**: Plotly支持多种图片格式（PNG、SVG、HTML），需要确定合适的格式
  - 缓解建议: 参考项目需求，通常PNG格式适合Web展示
  
- ⚠️ **文件夹路径管理**: 在不同环境（开发、Docker、生产）中路径可能不同
  - 缓解建议: 使用os.path.join和相对路径，参考player_info.py的路径处理方式
  
- ⚠️ **与现有/economy路由的集成**: economy.html模板可能为空或不完整，需要设计合适的UI展示物品价格和图表
  - 缓解建议: 先实现后端功能，再设计前端展示，保持与stats.html的风格一致
