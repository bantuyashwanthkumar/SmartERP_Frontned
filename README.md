# SmartERP: AI-Assisted Manufacturing ERP  
### Inventory | Procurement | Production | Warehouse | Approvals | AI Assistant

SmartERP is a full-stack, cloud-ready manufacturing ERP prototype built with **FastAPI**, **React + TypeScript**, and **PostgreSQL**. It connects core business processes such as sales orders, inventory, procurement, production, warehouse operations, approvals, finance, reporting, and an AI assistant.

The project demonstrates how an ERP system connects departments through one shared database and automated workflows. It is designed as a portfolio project for software engineering, ERP application development, backend development, full-stack development, QA automation, and ERP/product-support roles.

---

## Project Overview

In a manufacturing company, multiple teams work with the same business data:

- Sales creates customer orders.
- Inventory checks product and raw-material availability.
- Production plans manufacturing based on bills of materials.
- Procurement purchases missing materials from suppliers.
- Warehouse receives goods and updates stock.
- Finance records invoices, payments, costs, and liabilities.
- Managers monitor delays, stockouts, approvals, and supplier performance.

SmartERP connects these activities in one application.

Instead of maintaining separate Excel sheets or disconnected tools, the system uses a central PostgreSQL database. When inventory changes, procurement, production, warehouse, finance, and dashboards can access the updated information through APIs.

---

## Business Problem

Many small and mid-sized manufacturing companies manage operations using disconnected spreadsheets, emails, and separate applications.

This creates problems such as:

- Inventory records are outdated.
- Production teams discover material shortages too late.
- Purchase requests are delayed because approvals happen manually.
- Suppliers’ delivery status is not visible to production teams.
- Managers cannot easily see delayed orders, stockouts, or pending approvals.
- Important actions are not properly tracked in an audit trail.
- Reports require manual data collection from multiple sources.

SmartERP solves these problems by providing a connected ERP workflow with role-based access, approval management, real-time inventory updates, production tracking, procurement automation, and AI-assisted decision support.

---

## Key Features

### Authentication and Authorization

- User registration and login.
- JWT-based authentication.
- Access token and refresh token support.
- Role-based access control.
- Protected frontend and backend routes.
- Audit logging for important business actions.

### Master Data Management

- Products.
- Raw materials.
- Suppliers.
- Warehouses.
- Users.
- Roles and permissions.
- Bills of materials.
- Units of measure.
- Item categories.

### Inventory Management

- Stock quantity by product, raw material, warehouse, and location.
- Inventory transactions.
- Stock-in and stock-out movements.
- Safety-stock levels.
- Low-stock alerts.
- Reorder-point notifications.
- Stock-aging and movement history.
- Inventory reserved for sales and production orders.

### Sales Order Management

- Create customer sales orders.
- Add multiple products to an order.
- Check available finished-goods inventory.
- Reserve inventory for confirmed orders.
- Pick, pack, and ship orders.
- Generate customer invoices.
- Track order status from creation to delivery.

### Procurement Management

- Create purchase requisitions.
- Automatically detect material shortages.
- Send requisitions for approval.
- Approve or reject requisitions.
- Convert approved requisitions into purchase orders.
- Manage suppliers and supplier quotations.
- Track purchase-order status.
- Record goods receipts.
- Update inventory after material receipt.
- Create supplier invoices and pending liabilities.

### Production Management

- Create production orders.
- Define bills of materials.
- Calculate required raw materials.
- Check material availability.
- Create work orders.
- Issue raw materials to production.
- Track work-in-progress.
- Record production completion.
- Perform quality checks.
- Add finished goods to inventory.
- Track production delays and bottlenecks.

### Warehouse Management

- Manage warehouses and storage locations.
- Receive goods against purchase orders.
- Record inventory movements.
- Pick and pack sales orders.
- Track stock by warehouse and location.
- Maintain inventory transaction history.

### Approval Workflow

- Purchase requisition approval.
- Purchase order approval.
- Production order approval.
- Configurable approval limits.
- Approver comments.
- Approval history.
- Audit trail for every approval action.

### Finance and Reporting

- Customer invoices.
- Supplier invoices.
- Payments and receivables.
- Purchase costs.
- Production material costs.
- Pending supplier liabilities.
- Sales revenue reporting.
- Inventory valuation.

### Dashboard and Analytics

- Total sales orders.
- Open purchase orders.
- Pending approvals.
- Low-stock items.
- Delayed production orders.
- Delayed customer orders.
- Supplier on-time delivery percentage.
- Inventory turnover.
- Stockout risk.
- Production completion rate.
- Material shortage summary.

### AI Assistant

The AI assistant helps users understand ERP data and take action safely.

It can answer questions such as:

- “Which raw materials will run out this week?”
- “Why is production order PO-102 delayed?”
- “Show all delayed purchase orders.”
- “Which supplier has the lowest lead time for Raw Material X?”
- “Create a purchase requisition for 600 units of Raw Material X.”
- “Show pending approvals for the purchase manager.”

Important rule: the AI assistant can **read data and recommend actions**, but it cannot directly update ERP records. Every recommended action must be reviewed and approved by an authorized user.

### Human-in-the-Loop AI

The AI workflow is designed with safety and auditability in mind.

```text
User asks a question
        ↓
AI understands the intent
        ↓
AI retrieves relevant ERP data
        ↓
AI generates an answer and recommendation
        ↓
User reviews the recommendation
        ↓
User approves or rejects the action
        ↓
Approved action is executed through a controlled API
        ↓
Audit log records the action
```

---

## Technology Stack

### Backend

- Python 3.11+
- FastAPI
- Pydantic
- SQLAlchemy 2.0
- PostgreSQL
- Alembic
- JWT authentication
- Passlib / bcrypt
- Uvicorn
- Pytest
- Docker

### Frontend

- React 18+
- TypeScript
- Vite
- React Router
- Axios
- TanStack React Query
- React Hook Form
- Zod
- Tailwind CSS
- shadcn/ui or Material UI
- Recharts
- Vitest
- React Testing Library

### AI

- OpenAI API or Anthropic API
- Retrieval-Augmented Generation (RAG)
- Function calling / tool use
- Human approval workflow
- Audit trail

### DevOps

- Docker
- Docker Compose
- GitHub Actions
- PostgreSQL container
- Environment variables
- CI/CD pipeline
- Render, Railway, AWS, Azure, or any cloud platform

---

## System Architecture

```text
React + TypeScript Frontend
        ↓
Axios / REST API calls
        ↓
FastAPI Backend
        ↓
Service Layer
        ↓
Repository Layer
        ↓
SQLAlchemy ORM
        ↓
PostgreSQL Database

AI Assistant
        ↓
FastAPI AI Service
        ↓
LLM + RAG + ERP Data
        ↓
User Approval
        ↓
ERP Action API
```

---

## Folder Structure

```text
smarterp/
├── backend/
│   ├── app/
│   │   ├── main.py
│   │   ├── core/
│   │   │   ├── config.py
│   │   │   ├── security.py
│   │   │   ├── dependencies.py
│   │   │   └── exceptions.py
│   │   ├── db/
│   │   │   ├── base.py
│   │   │   ├── session.py
│   │   │   └── seed_data.py
│   │   ├── models/
│   │   │   ├── user.py
│   │   │   ├── role.py
│   │   │   ├── product.py
│   │   │   ├── raw_material.py
│   │   │   ├── supplier.py
│   │   │   ├── warehouse.py
│   │   │   ├── inventory.py
│   │   │   ├── inventory_transaction.py
│   │   │   ├── sales_order.py
│   │   │   ├── sales_order_line.py
│   │   │   ├── purchase_requisition.py
│   │   │   ├── purchase_requisition_line.py
│   │   │   ├── purchase_order.py
│   │   │   ├── purchase_order_line.py
│   │   │   ├── goods_receipt.py
│   │   │   ├── goods_receipt_line.py
│   │   │   ├── bill_of_material.py
│   │   │   ├── production_order.py
│   │   │   ├── production_order_material.py
│   │   │   ├── work_order.py
│   │   │   ├── quality_check.py
│   │   │   ├── invoice.py
│   │   │   ├── payment.py
│   │   │   ├── audit_log.py
│   │   │   ├── ai_conversation.py
│   │   │   └── ai_recommendation.py
│   │   ├── schemas/
│   │   │   ├── user.py
│   │   │   ├── auth.py
│   │   │   ├── product.py
│   │   │   ├── inventory.py
│   │   │   ├── supplier.py
│   │   │   ├── sales_order.py
│   │   │   ├── purchase_requisition.py
│   │   │   ├── purchase_order.py
│   │   │   ├── goods_receipt.py
│   │   │   ├── production_order.py
│   │   │   ├── invoice.py
│   │   │   ├── dashboard.py
│   │   │   └── ai.py
│   │   ├── api/
│   │   │   ├── v1/
│   │   │   │   ├── auth.py
│   │   │   │   ├── users.py
│   │   │   │   ├── products.py
│   │   │   │   ├── raw_materials.py
│   │   │   │   ├── suppliers.py
│   │   │   │   ├── warehouses.py
│   │   │   │   ├── inventory.py
│   │   │   │   ├── sales_orders.py
│   │   │   │   ├── purchase_requisitions.py
│   │   │   │   ├── purchase_orders.py
│   │   │   │   ├── goods_receipts.py
│   │   │   │   ├── production_orders.py
│   │   │   │   ├── bills_of_material.py
│   │   │   │   ├── work_orders.py
│   │   │   │   ├── quality_checks.py
│   │   │   │   ├── invoices.py
│   │   │   │   ├── dashboard.py
│   │   │   │   └── ai_assistant.py
│   │   │   └── router.py
│   │   ├── services/
│   │   │   ├── auth_service.py
│   │   │   ├── user_service.py
│   │   │   ├── inventory_service.py
│   │   │   ├── procurement_service.py
│   │   │   ├── production_service.py
│   │   │   ├── sales_service.py
│   │   │   ├── warehouse_service.py
│   │   │   ├── finance_service.py
│   │   │   ├── approval_service.py
│   │   │   ├── dashboard_service.py
│   │   │   └── ai_service.py
│   │   ├── repositories/
│   │   │   ├── base_repository.py
│   │   │   ├── user_repository.py
│   │   │   ├── product_repository.py
│   │   │   ├── inventory_repository.py
│   │   │   ├── procurement_repository.py
│   │   │   ├── production_repository.py
│   │   │   ├── sales_repository.py
│   │   │   └── dashboard_repository.py
│   │   ├── utils/
│   │   │   ├── pagination.py
│   │   │   ├── validators.py
│   │   │   └── date_utils.py
│   │   └── workers/
│   │       └── background_tasks.py
│   ├── alembic/
│   │   ├── versions/
│   │   └── env.py
│   ├── tests/
│   │   ├── conftest.py
│   │   ├── test_auth.py
│   │   ├── test_inventory.py
│   │   ├── test_procurement.py
│   │   ├── test_production.py
│   │   └── test_ai.py
│   ├── .env.example
│   ├── requirements.txt
│   ├── Dockerfile
│   └── alembic.ini
│
├── frontend/
│   ├── public/
│   ├── src/
│   │   ├── main.tsx
│   │   ├── App.tsx
│   │   ├── api/
│   │   │   ├── axiosClient.ts
│   │   │   ├── authApi.ts
│   │   │   ├── inventoryApi.ts
│   │   │   ├── procurementApi.ts
│   │   │   ├── productionApi.ts
│   │   │   ├── salesApi.ts
│   │   │   ├── dashboardApi.ts
│   │   │   └── aiApi.ts
│   │   ├── types/
│   │   │   ├── user.ts
│   │   │   ├── product.ts
│   │   │   ├── inventory.ts
│   │   │   ├── supplier.ts
│   │   │   ├── salesOrder.ts
│   │   │   ├── purchaseRequisition.ts
│   │   │   ├── purchaseOrder.ts
│   │   │   ├── productionOrder.ts
│   │   │   ├── dashboard.ts
│   │   │   └── ai.ts
│   │   ├── features/
│   │   │   ├── auth/
│   │   │   │   ├── components/
│   │   │   │   ├── hooks/
│   │   │   │   └── pages/
│   │   │   ├── dashboard/
│   │   │   ├── inventory/
│   │   │   ├── sales/
│   │   │   ├── procurement/
│   │   │   ├── warehouse/
│   │   │   ├── production/
│   │   │   ├── quality/
│   │   │   ├── finance/
│   │   │   ├── admin/
│   │   │   └── ai-assistant/
│   │   ├── components/
│   │   │   ├── ui/
│   │   │   ├── layout/
│   │   │   ├── tables/
│   │   │   ├── forms/
│   │   │   ├── charts/
│   │   │   └── common/
│   │   ├── hooks/
│   │   │   ├── useAuth.ts
│   │   │   ├── usePagination.ts
│   │   │   └── usePermissions.ts
│   │   ├── context/
│   │   │   └── AuthContext.tsx
│   │   ├── routes/
│   │   │   ├── AppRoutes.tsx
│   │   │   ├── ProtectedRoute.tsx
│   │   │   └── RoleRoute.tsx
│   │   ├── utils/
│   │   ├── constants/
│   │   └── styles/
│   ├── .env.example
│   ├── package.json
│   ├── tsconfig.json
│   ├── vite.config.ts
│   └── Dockerfile
│
├── docker-compose.yml
├── .github/
│   └── workflows/
│       └── ci.yml
├── docs/
│   ├── architecture.md
│   ├── er-diagram.png
│   ├── api-flow.md
│   └── business-workflow.md
└── README.md
```

---

## ERP Business Workflow

### Complete End-to-End Flow

```text
Customer places sales order
        ↓
Sales order created
        ↓
System checks finished-goods inventory
        ↓
Stock available?
        ↓
Yes → Reserve stock → Pick → Pack → Ship → Invoice
        ↓
No → Create production requirement
        ↓
Create production order
        ↓
Read bill of materials
        ↓
Calculate required raw materials
        ↓
Check raw-material inventory
        ↓
Materials available?
        ↓
Yes → Release production order → Issue materials → Produce → Quality check → Add finished goods
        ↓
No → Create purchase requisition
        ↓
Purchase manager approves requisition
        ↓
Buyer creates purchase order
        ↓
Supplier confirms and ships material
        ↓
Warehouse records goods receipt
        ↓
Inventory increases
        ↓
Production starts
        ↓
Raw materials are issued to production
        ↓
Finished goods are created
        ↓
Customer sales order is fulfilled
        ↓
Customer invoice is generated
```

---

## Detailed Workflow

### 1. Customer Places Order

A customer orders 500 units of Product A.

```text
Sales Order SO-501
Customer: XYZ Retail
Product: Product A
Quantity: 500 units
Status: Created
```

The system checks whether 500 finished units are available.

### 2. Inventory Check

If only 100 units are available:

```text
Required quantity: 500 units
Available quantity: 100 units
Shortage: 400 units
```

The system creates a production requirement.

### 3. Production Planning

The production planner creates a production order.

```text
Production Order PO-102
Product: Product A
Quantity: 500 units
Status: Planned
```

The system reads the bill of materials.

```text
To produce 500 units of Product A:
Raw Material X: 1,000 units
Component Y: 500 units
Machine M1: 2 hours
Labor: 10 hours
```

### 4. Material Shortage Detection

Suppose Raw Material X is short.

```text
Required Raw Material X: 1,000 units
Available Raw Material X: 400 units
Shortage: 600 units
```

The system creates a purchase requisition.

```text
Purchase Requisition PR-201
Item: Raw Material X
Quantity: 600 units
Required Date: 20 November
Requested By: Production Planner
Reason: Production Order PO-102
Status: Pending Approval
```

### 5. Requisition Approval

The purchase manager reviews the requisition.

```text
PR-201
Amount: ₹1,20,000
Approver: Purchase Manager
Status: Pending Approval
```

After approval:

```text
PR-201
Status: Approved
Approved By: Purchase Manager
Approved At: 17 November 2026
```

### 6. Purchase Order Creation

The buyer converts the approved requisition into a purchase order.

```text
Purchase Order PO-301
Supplier: ABC Materials
Item: Raw Material X
Quantity: 600 units
Expected Delivery: 18 November
Status: Sent to Supplier
```

### 7. Supplier Shipment

The supplier confirms the order and ships the material.

```text
PO-301
Status: Shipped
Expected Delivery: 18 November
```

### 8. Goods Receipt

When the material arrives, the warehouse user records a goods receipt.

```text
Goods Receipt GR-401
Purchase Order: PO-301
Item: Raw Material X
Received Quantity: 600 units
Warehouse: Main Warehouse
Status: Received
```

Inventory is updated:

```text
Before receipt:
Raw Material X = 400 units

After receipt:
Raw Material X = 1,000 units
```

### 9. Production Execution

Production can now begin.

```text
Production Order PO-102
Status: Released
Required Materials: Available
```

During production:

```text
Raw Material X issued: 1,000 units
Raw Material X inventory: 1,000 → 0 units
Work-in-progress increases
Production order progresses
```

After quality checks:

```text
Finished Product A added: 500 units
Product A inventory: 100 → 600 units
```

### 10. Sales Fulfillment

The sales order can now be fulfilled.

```text
SO-501
Status: Ready to Ship
Product A available: 600 units
Required: 500 units
```

The warehouse picks, packs, and ships the order.

```text
Product A inventory: 600 → 100 units
SO-501 Status: Shipped
Invoice generated
```

---

## AI Assistant Workflow

```text
User asks: “Which raw materials will be short for Production Order PO-102?”
        ↓
Frontend sends request to POST /api/v1/ai/ask
        ↓
FastAPI AI service receives question
        ↓
AI identifies intent
        ↓
AI retrieves ERP data
        ↓
AI analyzes BOM, inventory, purchase orders, and supplier lead time
        ↓
AI generates answer
        ↓
AI creates recommendation
        ↓
User reviews recommendation
        ↓
User approves or rejects
        ↓
Approved action executes
        ↓
Audit log is created
```

### Example AI Interaction

```text
User:
Which raw materials will be short for Production Order PO-102?

AI:
Production Order PO-102 requires 1,000 units of Raw Material X.
Current available stock is 400 units.
Shortage: 600 units.
Supplier ABC Materials can deliver by 18 November.

Recommended Action:
Create a purchase requisition for 600 units of Raw Material X.

[Approve] [Reject]
```

If the user approves:

```text
Purchase Requisition PR-201 created.
Status: Pending Approval.
Created By: AI Assistant.
Approved By: User.
Audit Log: AI recommendation approved.
```

---

## Database Design

### Core Tables

```text
users
roles
user_roles

products
raw_materials
suppliers
warehouses
inventory
inventory_transactions

sales_orders
sales_order_lines

purchase_requisitions
purchase_requisition_lines
purchase_orders
purchase_order_lines
goods_receipts
goods_receipt_lines

bill_of_materials
production_orders
production_order_materials
work_orders
quality_checks

invoices
payments

audit_logs
ai_conversations
ai_recommendations
```

### Important Relationships

```text
User ──< SalesOrder
SalesOrder ──< SalesOrderLine >── Product

Product ──< BillOfMaterial >── RawMaterial

SalesOrder ──< ProductionOrder
ProductionOrder ──< ProductionOrderMaterial >── RawMaterial

ProductionOrderMaterial ──< PurchaseRequisition
PurchaseRequisition ──< PurchaseOrder
PurchaseOrder ──< GoodsReceipt
GoodsReceipt ──< InventoryTransaction

Product / RawMaterial ──< Inventory >── Warehouse
```

---

## Backend API Endpoints

### Authentication

```http
POST /api/v1/auth/register
POST /api/v1/auth/login
POST /api/v1/auth/refresh
GET  /api/v1/auth/me
```

### Users and Roles

```http
GET    /api/v1/users
POST   /api/v1/users
GET    /api/v1/users/{id}
PUT    /api/v1/users/{id}
DELETE /api/v1/users/{id}

GET    /api/v1/roles
POST   /api/v1/roles
```

### Products and Materials

```http
GET    /api/v1/products
POST   /api/v1/products
GET    /api/v1/products/{id}
PUT    /api/v1/products/{id}
DELETE /api/v1/products/{id}

GET    /api/v1/raw-materials
POST   /api/v1/raw-materials
GET    /api/v1/raw-materials/{id}
PUT    /api/v1/raw-materials/{id}
```

### Inventory

```http
GET  /api/v1/inventory
GET  /api/v1/inventory/{id}
GET  /api/v1/inventory/low-stock
GET  /api/v1/inventory/transactions
POST /api/v1/inventory/adjust
```

### Sales Orders

```http
GET  /api/v1/sales-orders
POST /api/v1/sales-orders
GET  /api/v1/sales-orders/{id}
PUT  /api/v1/sales-orders/{id}
POST /api/v1/sales-orders/{id}/allocate
POST /api/v1/sales-orders/{id}/ship
POST /api/v1/sales-orders/{id}/invoice
```

### Procurement

```http
GET  /api/v1/purchase-requisitions
POST /api/v1/purchase-requisitions
GET  /api/v1/purchase-requisitions/{id}
PATCH /api/v1/purchase-requisitions/{id}/approve
PATCH /api/v1/purchase-requisitions/{id}/reject

GET  /api/v1/purchase-orders
POST /api/v1/purchase-orders
GET  /api/v1/purchase-orders/{id}
PATCH /api/v1/purchase-orders/{id}/send
PATCH /api/v1/purchase-orders/{id}/receive
```

### Goods Receipt

```http
GET  /api/v1/goods-receipts
POST /api/v1/goods-receipts
GET  /api/v1/goods-receipts/{id}
```

### Production

```http
GET  /api/v1/production-orders
POST /api/v1/production-orders
GET  /api/v1/production-orders/{id}
PATCH /api/v1/production-orders/{id}/release
PATCH /api/v1/production-orders/{id}/issue-materials
PATCH /api/v1/production-orders/{id}/complete

GET  /api/v1/bills-of-material
POST /api/v1/bills-of-material

GET  /api/v1/work-orders
POST /api/v1/work-orders

GET  /api/v1/quality-checks
POST /api/v1/quality-checks
```

### Finance

```http
GET  /api/v1/invoices
POST /api/v1/invoices
GET  /api/v1/invoices/{id}
POST /api/v1/invoices/{id}/payment
```

### Dashboard

```http
GET /api/v1/dashboard/kpis
GET /api/v1/dashboard/low-stock
GET /api/v1/dashboard/delayed-orders
GET /api/v1/dashboard/pending-approvals
GET /api/v1/dashboard/supplier-performance
```

### AI Assistant

```http
POST /api/v1/ai/ask
GET  /api/v1/ai/conversations
GET  /api/v1/ai/recommendations
POST /api/v1/ai/recommendations/{id}/approve
POST /api/v1/ai/recommendations/{id}/reject
```

---

## Backend Service Layer

The backend should not place all logic inside API route files. Use separate layers.

```text
API Route
   ↓
Schema Validation
   ↓
Service Layer
   ↓
Repository Layer
   ↓
Database Model
   ↓
PostgreSQL
```

### Example: Procurement Service

```python
# backend/app/services/procurement_service.py

from app.repositories.procurement_repository import ProcurementRepository
from app.services.inventory_service import InventoryService
from app.models.purchase_requisition import PurchaseRequisition
from app.core.exceptions import BusinessRuleError

class ProcurementService:
    def __init__(
        self,
        procurement_repository: ProcurementRepository,
        inventory_service: InventoryService,
    ):
        self.procurement_repository = procurement_repository
        self.inventory_service = inventory_service

    def create_requisition_from_shortage(
        self,
        production_order_id: int,
        material_id: int,
        required_quantity: float,
    ):
        available_quantity = self.inventory_service.get_available_quantity(
            material_id
        )

        shortage_quantity = required_quantity - available_quantity

        if shortage_quantity <= 0:
            raise BusinessRuleError("No material shortage found.")

        requisition = PurchaseRequisition(
            production_order_id=production_order_id,
            material_id=material_id,
            quantity=shortage_quantity,
            status="PENDING_APPROVAL",
        )

        return self.procurement_repository.create(requisition)
```

### Example: Approval Service

```python
# backend/app/services/approval_service.py

from app.core.exceptions import BusinessRuleError

class ApprovalService:
    def approve_requisition(self, requisition, approver):
        if requisition.status != "PENDING_APPROVAL":
            raise BusinessRuleError(
                "Only pending requisitions can be approved."
            )

        if approver.role != "PURCHASE_MANAGER":
            raise BusinessRuleError(
                "Only purchase managers can approve requisitions."
            )

        requisition.status = "APPROVED"
        requisition.approved_by = approver.id
        return requisition
```

---

## Frontend Architecture

The React frontend uses a feature-based structure.

```text
src/
├── api/
├── types/
├── features/
├── components/
├── hooks/
├── context/
├── routes/
├── utils/
└── constants/
```

### API Client

```typescript
// frontend/src/api/axiosClient.ts

import axios from "axios";

const axiosClient = axios.create({
  baseURL: import.meta.env.VITE_API_BASE_URL,
  timeout: 20000,
});

axiosClient.interceptors.request.use((config) => {
  const token = localStorage.getItem("access_token");

  if (token) {
    config.headers.Authorization = `Bearer ${token}`;
  }

  return config;
});

axiosClient.interceptors.response.use(
  (response) => response,
  async (error) => {
    if (error.response?.status === 401) {
      localStorage.removeItem("access_token");
      window.location.href = "/login";
    }

    return Promise.reject(error);
  }
);

export default axiosClient;
```

### Example API Function

```typescript
// frontend/src/api/procurementApi.ts

import axiosClient from "./axiosClient";
import { PurchaseRequisition } from "../types/purchaseRequisition";

export const getPurchaseRequisitions = async (): Promise<
  PurchaseRequisition[]
> => {
  const response = await axiosClient.get("/api/v1/purchase-requisitions");
  return response.data;
};

export const approvePurchaseRequisition = async (
  requisitionId: number
): Promise<PurchaseRequisition> => {
  const response = await axiosClient.patch(
    `/api/v1/purchase-requisitions/${requisitionId}/approve`
  );

  return response.data;
};
```

### Example React Query Hook

```typescript
// frontend/src/features/procurement/hooks/usePurchaseRequisitions.ts

import { useQuery } from "@tanstack/react-query";
import { getPurchaseRequisitions } from "../../../api/procurementApi";

export const usePurchaseRequisitions = () => {
  return useQuery({
    queryKey: ["purchase-requisitions"],
    queryFn: getPurchaseRequisitions,
  });
};
```

### Example React Component

```tsx
// frontend/src/features/procurement/pages/PurchaseRequisitionList.tsx

import { usePurchaseRequisitions } from "../hooks/usePurchaseRequisitions";
import { RequisitionStatusBadge } from "../components/RequisitionStatusBadge";

export default function PurchaseRequisitionList() {
  const { data, isLoading, error } = usePurchaseRequisitions();

  if (isLoading) return <p>Loading requisitions...</p>;

  if (error) return <p>Unable to load requisitions.</p>;

  return (
    <div>
      <h1>Purchase Requisitions</h1>

      <table>
        <thead>
          <tr>
            <th>Requisition</th>
            <th>Material</th>
            <th>Quantity</th>
            <th>Status</th>
          </tr>
        </thead>

        <tbody>
          {data?.map((requisition) => (
            <tr key={requisition.id}>
              <td>{requisition.requisition_number}</td>
              <td>{requisition.material_name}</td>
              <td>{requisition.quantity}</td>
              <td>
                <RequisitionStatusBadge status={requisition.status} />
              </td>
            </tr>
          ))}
        </tbody>
      </table>
    </div>
  );
}
```

---

## User Roles

```text
ADMIN
├── Manage users, roles, permissions, and master data

SALES_USER
├── Create sales orders
├── Check inventory
├── Ship orders
└── Generate invoices

PRODUCTION_PLANNER
├── Create production orders
├── Check BOM and material availability
├── Release work orders
└── Track production progress

PURCHASE_MANAGER
├── Approve or reject purchase requisitions
└── Monitor procurement performance

BUYER
├── Create purchase orders
├── Manage suppliers
└── Track supplier deliveries

WAREHOUSE_USER
├── Receive goods
├── Manage inventory
├── Pick and pack orders
└── Ship orders

QUALITY_USER
├── Perform quality checks
└── Approve or reject production output

FINANCE_USER
├── View invoices
├── Track payments
└── Monitor costs and liabilities
```

---

## Environment Variables

### Backend `.env.example`

```env
DATABASE_URL=postgresql://postgres:postgres@localhost:5432/smarterp
SECRET_KEY=your-secret-key
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=30
REFRESH_TOKEN_EXPIRE_DAYS=7
CORS_ORIGINS=http://localhost:5173
OPENAI_API_KEY=your-openai-api-key
```

### Frontend `.env.example`

```env
VITE_API_BASE_URL=http://localhost:8000
```

---

## Installation

### Prerequisites

Install the following:

- Python 3.11+
- Node.js 18+
- PostgreSQL 14+
- Docker
- Docker Compose
- Git

### Clone Repository

```bash
git clone [https://github.com/your-username/smarterp.git](https://github.com/your-username/smarterp.git)
cd smarterp
```

---

## Backend Setup

### Create Virtual Environment

```bash
cd backend
python -m venv venv
source venv/bin/activate
```

For Windows:

```bash
venv\Scripts\activate
```

### Install Dependencies

```bash
pip install -r requirements.txt
```

### Configure Environment

```bash
cp .env.example .env
```

Update the database URL and secret key.

### Run Database Migrations

```bash
alembic upgrade head
```

### Seed Demo Data

```bash
python -m app.db.seed_data
```

### Start Backend

```bash
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

Backend will run at:

```text
http://localhost:8000
```

API documentation:

```text
http://localhost:8000/docs
```

---

## Frontend Setup

### Install Dependencies

```bash
cd frontend
npm install
```

### Configure Environment

```bash
cp .env.example .env
```

### Start Frontend

```bash
npm run dev
```

Frontend will run at:

```text
http://localhost:5173
```

---

## Docker Setup

### Start All Services

```bash
docker-compose up --build
```

### Stop Services

```bash
docker-compose down
```

### Rebuild Containers

```bash
docker-compose up --build -d
```

---

## Docker Compose Example

```yaml
version: "3.9"

services:
  db:
    image: postgres:16
    container_name: smarterp-db
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres
      POSTGRES_DB: smarterp
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data

  backend:
    build:
      context: ./backend
    container_name: smarterp-backend
    environment:
      DATABASE_URL: postgresql://postgres:postgres@db:5432/smarterp
      SECRET_KEY: change-this-secret
      CORS_ORIGINS: http://localhost:5173
    ports:
      - "8000:8000"
    depends_on:
      - db

  frontend:
    build:
      context: ./frontend
    container_name: smarterp-frontend
    environment:
      VITE_API_BASE_URL: http://localhost:8000
    ports:
      - "5173:5173"
    depends_on:
      - backend

volumes:
  postgres_data:
```

---

## Testing

### Backend Tests

```bash
cd backend
pytest -v
```

### Frontend Tests

```bash
cd frontend
npm run test
```

### API Testing

Use:

- Postman
- Insomnia
- FastAPI Swagger UI
- Newman
- REST Assured

---

## Project Screenshots

Add screenshots here after building the UI:

```text
1. Login Page
2. Dashboard
3. Inventory Dashboard
4. Sales Order Creation
5. Production Order
6. Purchase Requisition Approval
7. Purchase Order Details
8. Goods Receipt
9. AI Assistant Chat
10. Audit Log
```

---

## Demo Credentials

```text
Admin:
Email: admin@smarterp.com
Password: Admin@123

Production Planner:
Email: planner@smarterp.com
Password: Planner@123

Purchase Manager:
Email: manager@smarterp.com
Password: Manager@123

Warehouse User:
Email: warehouse@smarterp.com
Password: Warehouse@123
```

Do not expose real credentials in a public repository.

---

## Future Enhancements

- Multi-company and multi-currency support.
- Advanced MRP and demand forecasting.
- Supplier portal.
- Barcode and QR-code scanning.
- Mobile warehouse application.
- Real-time notifications using WebSockets.
- Advanced role-based permissions.
- Automated supplier quotation comparison.
- Predictive inventory planning.
- Production scheduling optimization.
- Advanced financial reporting.
- Integration with payment gateways.
- Integration with shipping providers.
- Advanced AI agents for autonomous ERP workflows.

---

## Learning Outcomes

By building SmartERP, you demonstrate:

- Full-stack application development.
- REST API design.
- PostgreSQL database modeling.
- Authentication and authorization.
- Role-based access control.
- ERP business-process understanding.
- Inventory and procurement workflows.
- Production and warehouse workflows.
- Approval workflows.
- Audit logging.
- AI integration with human-in-the-loop controls.
- React and TypeScript frontend development.
- Docker and cloud deployment.
- Testing and documentation.

---

## Resume Project Description

```text
SmartERP: AI-Assisted Manufacturing ERP
Built a full-stack manufacturing ERP prototype using FastAPI, React TypeScript, 
and PostgreSQL. Implemented inventory, procurement, production, warehouse, sales, 
approval, and reporting workflows. Designed REST APIs for sales orders, purchase 
requisitions, purchase orders, goods receipts, bills of materials, and production 
orders. Added role-based access control, audit logging, and an AI assistant that 
recommends ERP actions with mandatory human approval before execution. 
Containerized the application with Docker and automated build and deployment 
using GitHub Actions.
```

---

## GitHub Repository Description

```text
SmartERP is an AI-assisted manufacturing ERP built with FastAPI, React TypeScript, 
and PostgreSQL. It connects inventory, procurement, production, warehouse, approvals, 
finance, and AI-assisted decision support in one end-to-end business workflow.
```

---

## License

This project is for educational and portfolio purposes.

---

## Author

Your Name  
GitHub: https://github.com/your-username  
LinkedIn: https://www.linkedin.com/in/your-username  
Portfolio: https://your-portfolio-link.com  
