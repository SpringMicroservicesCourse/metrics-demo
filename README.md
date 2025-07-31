# Spring Boot 微服務監控系統 ⚡

[![Java](https://img.shields.io/badge/Java-21-orange.svg)](https://www.oracle.com/java/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.4.5-brightgreen.svg)](https://spring.io/projects/spring-boot)
[![Maven](https://img.shields.io/badge/Maven-3.8+-red.svg)](https://maven.apache.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## 專案介紹

這是一個基於 Spring Boot 3.x 的微服務監控系統示範專案，主要展示如何在 Spring Boot 應用程式中整合 Micrometer 來收集各種度量指標。專案模擬了一個咖啡廳訂單系統，透過實際的業務場景來演示監控系統的實作。

> 💡 **為什麼選擇此專案？**
> - 完整展示 Spring Boot 3.x 與 Micrometer 的整合
> - 提供實際的業務場景作為監控示範
> - 包含完整的健康檢查和度量指標收集
> - 支援多種監控系統（Prometheus、Grafana 等）

### 🎯 專案特色

- **完整的監控體系**：整合 Spring Boot Actuator 和 Micrometer
- **業務指標收集**：自動收集訂單數量、API 響應時間等業務指標
- **健康檢查機制**：自定義健康檢查指標，確保系統穩定運行
- **效能監控**：透過攔截器收集 API 呼叫的詳細效能資料
- **多維度度量**：支援標籤（Tag）功能，實現多維度監控

## 技術棧

### 核心框架
- **Spring Boot 3.4.5** - 現代化的 Java 應用程式框架
- **Spring Data JPA** - 資料持久化層，簡化資料庫操作
- **Spring Web MVC** - RESTful API 開發框架
- **Spring Boot Actuator** - 應用程式監控和管理端點

### 監控與度量
- **Micrometer** - 度量指標收集的核心框架
- **Micrometer Registry Prometheus** - Prometheus 監控系統整合
- **Spring Boot Actuator** - 健康檢查和監控端點

### 開發工具與輔助
- **Lombok** - 減少樣板程式碼，提升開發效率
- **H2 Database** - 內嵌式資料庫，方便開發和測試
- **Joda Money** - 貨幣處理庫，確保金額計算的準確性
- **Apache Commons Lang3** - 常用工具類庫

## 專案結構

```
metrics-demo/
├── src/
│   ├── main/
│   │   ├── java/tw/fengqing/spring/springbucks/waiter/
│   │   │   ├── WaiterServiceApplication.java          # 應用程式主類別
│   │   │   ├── controller/                            # 控制器層
│   │   │   │   ├── CoffeeController.java             # 咖啡管理 API
│   │   │   │   ├── CoffeeOrderController.java        # 訂單管理 API
│   │   │   │   ├── PerformanceInteceptor.java        # 效能監控攔截器
│   │   │   │   └── request/                          # 請求物件
│   │   │   ├── model/                                # 資料模型層
│   │   │   │   ├── BaseEntity.java                   # 基礎實體類別
│   │   │   │   ├── Coffee.java                       # 咖啡實體
│   │   │   │   ├── CoffeeOrder.java                  # 訂單實體
│   │   │   │   ├── OrderState.java                   # 訂單狀態列舉
│   │   │   │   └── MoneyConverter.java               # 貨幣轉換器
│   │   │   ├── repository/                           # 資料存取層
│   │   │   │   ├── CoffeeRepository.java             # 咖啡資料存取
│   │   │   │   └── CoffeeOrderRepository.java        # 訂單資料存取
│   │   │   ├── service/                              # 業務邏輯層
│   │   │   │   ├── CoffeeService.java                # 咖啡業務邏輯
│   │   │   │   └── CoffeeOrderService.java           # 訂單業務邏輯
│   │   │   └── support/                              # 支援類別
│   │   │       ├── CoffeeIndicator.java              # 自定義健康檢查
│   │   │       ├── MoneyDeserializer.java            # 貨幣反序列化器
│   │   │       ├── MoneyFormatter.java               # 貨幣格式化器
│   │   │       └── MoneySerializer.java              # 貨幣序列化器
│   │   └── resources/
│   │       ├── application.properties                 # 應用程式設定檔
│   │       ├── schema.sql                            # 資料庫結構定義
│   │       ├── data.sql                              # 初始資料
│   │       └── coffee.txt                            # 咖啡資料檔案
│   └── test/                                         # 測試程式碼
├── pom.xml                                           # Maven 專案設定
└── README.md                                         # 專案說明文件
```

## 快速開始

### 前置需求
- **Java 21** - 確保已安裝 JDK 21 或更新版本
- **Maven 3.8+** - 專案建置工具
- **IDE 支援** - 建議使用 IntelliJ IDEA 或 Eclipse

### 安裝與執行

1. **克隆此倉庫：**
```bash
git clone https://github.com/SpringMicroservicesCourse/spring-microservices-course.git
```

2. **進入專案目錄：**
```bash
cd metrics-demo
```

3. **編譯專案：**
```bash
mvn clean compile
```

4. **執行應用程式：**
```bash
mvn spring-boot:run
```

5. **驗證應用程式：**
   - 應用程式將在 `http://localhost:8080` 啟動
   - 健康檢查端點：`http://localhost:8080/actuator/health`
   - 度量指標端點：`http://localhost:8080/actuator/metrics`

## API 端點說明

### 咖啡管理 API
- `GET /coffee/` - 取得所有咖啡清單
- `GET /coffee/{id}` - 根據 ID 取得咖啡資訊
- `GET /coffee/?name={name}` - 根據名稱取得咖啡資訊
- `POST /coffee/` - 新增咖啡（支援 JSON 和表單格式）
- `POST /coffee/` (multipart) - 批次新增咖啡

### 訂單管理 API
- `GET /order/{id}` - 根據 ID 取得訂單資訊
- `POST /order/` - 建立新訂單

### 監控端點
- `GET /actuator/health` - 應用程式健康狀態
- `GET /actuator/metrics` - 所有可用度量指標
- `GET /actuator/metrics/{metric.name}` - 特定度量指標詳情
- `GET /actuator/prometheus` - Prometheus 格式的度量指標

## 進階說明

### 環境變數
```properties
# 資料庫設定
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driver-class-name=org.h2.Driver

# JPA 設定
spring.jpa.hibernate.ddl-auto=none
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true

# Actuator 設定
management.endpoints.web.exposure.include=*
management.endpoint.health.show-details=always

# 應用程式資訊
info.app.author=DigitalSonic
info.app.encoding=@project.build.sourceEncoding@
```

### 自定義度量指標

專案中實作了自定義的度量指標收集：

```java
// 在 CoffeeOrderService 中實作 MeterBinder 介面
@Override
public void bindTo(MeterRegistry meterRegistry) {
    // 註冊訂單計數器
    this.orderCounter = meterRegistry.counter("order.count");
}
```

### 效能監控攔截器

透過 `PerformanceInteceptor` 收集 API 呼叫的詳細效能資料：

```java
@Override
public void afterCompletion(HttpServletRequest request, 
                          HttpServletResponse response, 
                          Object handler, 
                          Exception ex) throws Exception {
    // 記錄 API 呼叫的詳細資訊
    log.info("{};{};{};{};{}ms;{}ms;{}ms", 
             request.getRequestURI(), method,
             response.getStatus(), 
             ex == null ? "-" : ex.getClass().getSimpleName(),
             sw.getTotalTimeMillis(), 
             sw.getTotalTimeMillis() - sw.getLastTaskTimeMillis(),
             sw.getLastTaskTimeMillis());
}
```

## 監控系統整合

### Prometheus 整合
專案已整合 Prometheus 監控系統，可透過以下端點取得度量指標：
- `GET /actuator/prometheus` - 取得 Prometheus 格式的度量指標

### Grafana 儀表板
建議搭配 Grafana 建立監控儀表板，監控以下指標：
- 應用程式健康狀態
- API 響應時間
- 訂單數量統計
- 系統資源使用情況

## 參考資源

- [Spring Boot 官方文件](https://spring.io/projects/spring-boot)
- [Micrometer 官方文件](https://micrometer.io/)
- [Spring Boot Actuator 文件](https://docs.spring.io/spring-boot/docs/current/reference/html/actuator.html)
- [Prometheus 官方文件](https://prometheus.io/docs/)

## 注意事項與最佳實踐

### ⚠️ 重要提醒

| 項目 | 說明 | 建議做法 |
|------|------|----------|
| 版本相容性 | Spring Boot 3.x 使用 Jakarta EE | 確保所有依賴都支援 Jakarta EE |
| 度量指標收集 | 避免過度收集影響效能 | 只收集關鍵業務指標 |
| 資料庫連線 | 使用連線池提升效能 | 配置適當的連線池大小 |
| 安全性 | 生產環境需保護監控端點 | 使用 Spring Security 保護 Actuator 端點 |

### 🔒 最佳實踐指南

- **度量指標設計**：遵循命名規範，使用點分隔的命名方式
- **標籤使用**：合理使用標籤進行多維度分析，避免標籤基數過高
- **效能考量**：避免在高頻呼叫的程式碼中進行複雜的度量計算
- **監控策略**：建立完整的監控告警機制，及時發現問題

### 📝 程式碼註解規範

專案中所有重要的程式碼區塊都包含清楚的註解：

```java
/**
 * JPA 屬性轉換器
 * 用於在資料庫和 Java 物件之間轉換 Money 類型
 */
@Converter(autoApply = true)
public class MoneyConverter implements AttributeConverter<Money, Long> {
    
    /**
     * 將 Money 物件轉換為資料庫中的長整數值
     * 將金額轉換為最小貨幣單位（分）
     * 
     * @param attribute Money 物件
     * @return 轉換後的長整數值
     */
    @Override
    public Long convertToDatabaseColumn(Money attribute) {
        return attribute == null ? null : attribute.getAmountMinorLong();
    }
}
```

## 授權說明

本專案採用 MIT 授權條款，詳見 LICENSE 檔案。

## 關於我們

我們主要專注在敏捷專案管理、物聯網（IoT）應用開發和領域驅動設計（DDD）。喜歡把先進技術和實務經驗結合，打造好用又靈活的軟體解決方案。

## 聯繫我們

- **FB 粉絲頁**：[風清雲談 | Facebook](https://www.facebook.com/profile.php?id=61576838896062)
- **LinkedIn**：[linkedin.com/in/chu-kuo-lung](https://www.linkedin.com/in/chu-kuo-lung)
- **YouTube 頻道**：[雲談風清 - YouTube](https://www.youtube.com/channel/UCXDqLTdCMiCJ1j8xGRfwEig)
- **風清雲談 部落格**：[風清雲談](https://blog.fengqing.tw/)
- **電子郵件**：[fengqing.tw@gmail.com](mailto:fengqing.tw@gmail.com)

---

**📅 最後更新：2025-07-31**  
**👨‍💻 維護者：風清雲談團隊** 