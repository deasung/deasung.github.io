---

title: QueryDSL Projections.bean
published: true
---


쿼리 결과를 엔티티가 아닌 특정한 자바객체(DTO, VO)로 받고 싶은 경우 Pjojections를 사용하면 되는데 .bean()을 사용하면 Setter로 값을 채우고 .field()라고 하면 필드(멤버변수)에 직접 접근하여 값을 채우며, .constructor() 라고 하면 생성자를 통해 값을 채운다.

```java
.select(Projections.bean(
  OrderRefundProcDTO_orderProduct_info.class
  , $q_orderProduct.id.as("orderProductId")
  , $q_orderProduct.orderStatusCd.as("orderStatusCd")
  , $q_orderProduct.orderCancellationCd.as("orderCancellationCd")
  , $q_orderProduct.deliveryType.as("deliveryType")
  , $q_orderProduct.price.as("price")
  , $q_orderProduct.quantity.as("quantity")
  , $q_supplier.name.as("supplierName")
  , $q_productGoods.id.as("productGoodsId")
  , $q_product.id.as("productId")
  , $q_product.name.as("productName")
  , $q_productMeta.representImageUrl.as("productImage")
  , $q_supplier.id.as("supplierId")
  , $q_orderProduct.deliveryCharge.as("deliveryCharge")
  ))
```