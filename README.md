# Project XØ — Voice Cloning Fraud Detection

Raksham Hackathon, IIT Delhi.

**Pitch:** Real-time detection of cloned-voice scam calls, with an explainable risk score that combines audio forensics and scam-language analysis.

## Team
| Member | Role |
|---|---|
| Het (lead) | AI / ML |
| Ishrit | Frontend & UI/UX |
| Vasu | Backend & Integration |
| Gopani | Testing, Security & Demo |

## Repo layout
```
ml/          model code (features, training, augmentation, predict)
backend/     FastAPI server (mock mode by default, real mode when model exists)
frontend/    UI (a simple test page is included; Ishrit builds the real one)
tests/       API tests
docs/        API contract, results, team plan
data/        datasets (git-ignored)
```

## Quick start
```bash
python -m venv venv
venv\Scripts\activate            # Windows  (Linux/Mac: source venv/bin/activate)
pip install -r requirements.txt

# run backend in MOCK mode (works with no model)
uvicorn backend.main:app --reload
# open frontend/index.html in a browser to test
```

Switch to the real model after training:
```bash
set XO_MODE=real                 # Windows  (Linux/Mac: export XO_MODE=real)
uvicorn backend.main:app --reload
```

## ML workflow
1. Put audio in `data/` and build manifests: `python -m ml.make_manifest --help`
2. Extract features: `python -m ml.build_features --manifest data/train.csv --out data/train`
3. Train + EER: `python -m ml.train`
4. Telephony robustness: `python -m ml.augment --help`
5. Results go in `docs/results.md`

## Team rules
- Only use **consented** voices for cloning/test data.
- Never commit datasets, models or raw voice recordings.
- API contract is in `docs/api_contract.md`. Change it only after telling everyone.
