# Folder Structure

## Source repository structure (verified)
```text
mrm/
├── apps/
│   ├── client/
│   │   ├── public/
│   │   ├── src/
│   │   │   ├── api/
│   │   │   ├── assets/
│   │   │   ├── components/
│   │   │   │   ├── Layout/
│   │   │   │   ├── common/
│   │   │   │   └── ui/
│   │   │   ├── config/
│   │   │   ├── context/
│   │   │   ├── hooks/
│   │   │   ├── lib/
│   │   │   ├── pages/
│   │   │   │   ├── auth/
│   │   │   │   ├── common/
│   │   │   │   ├── customer/
│   │   │   │   ├── payments/
│   │   │   │   ├── repairOrder/
│   │   │   │   ├── reports/
│   │   │   │   ├── settings/
│   │   │   │   ├── superadmin/
│   │   │   │   ├── supplier/
│   │   │   │   ├── technician/
│   │   │   │   ├── users/
│   │   │   │   └── website/
│   │   │   ├── utils/
│   │   │   ├── App.jsx
│   │   │   └── main.jsx
│   │   ├── package.json
│   │   ├── tailwind.config.js
│   │   └── vite.config.js
│   └── server/
│       ├── blueprints/
│       ├── config/
│       ├── controllers/
│       ├── middleware/
│       ├── models/
│       ├── routes/
│       │   └── platformRoutes/
│       ├── scripts/
│       ├── services/
│       ├── utils/
│       ├── app.js
│       ├── server.js
│       └── package.json
├── packages/
│   └── validators/
│       ├── src/
│       │   ├── constants/
│       │   └── schemas/
│       └── package.json
├── package.json
└── turbo.json
```

## Rebuild rule
Preserve these package boundaries initially. Architectural cleanup should happen only after functional parity is demonstrated, because shared validators and tenant-scoping assumptions cross package boundaries.

## Still to extract
A complete file-by-file manifest for every page, component, controller, utility, config file, service, schema and constant remains an active reconstruction task and is tracked in `reconstruction/manifests/FILE-MANIFEST.md`.
