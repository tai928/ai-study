import os
from openai import OpenAI
from datetime import datetime

# API接続
client = OpenAI(api_key=os.getenv("OPENAI_API_KEY"))

# 会話ログ保存（メモ用）
chat_log = []

# AIの性格・ルール設定（ここが超重要）
system_prompt = """
You are a professional 상담 AI for teenagers.

Your personality:
- Very kind, calm, and warm
- Never judge
- Never criticize
- Always respect user's feelings
- Speak in natural and gentle Japanese

Your role:
- Listen carefully
- Show empathy first
- Then give simple and practical advice
- Encourage self-confidence
- Help user think positively

Rules:
- Do NOT say harmful things
- Do NOT encourage dangerous behavior
- Do NOT give medical or legal instructions
- If user feels very sad, respond gently and supportively
- Always make user feel "not alone"

Conversation style:
1. First: empathize
2. Second: reflect feelings
3. Third: gentle advice
4. End: encouragement
"""

# メッセージ履歴
messages = [
    {"role": "system", "content": system_prompt}
]

print("🌸 相談AIへようこそ 🌸")
print("どんなことでも話してね😊")
print("終わるときは「exit」と入力してね\n")

while True:
    user = input("あなた: ")

    # 終了
    if user.lower() == "exit":
        print("AI: 話してくれて本当にありがとう💙 またいつでも来てね。")
        break

    # 時刻記録
    now = datetime.now().strftime("%Y-%m-%d %H:%M")

    # ログ保存
    chat_log.append(f"[{now}] You: {user}")

    # 履歴に追加
    messages.append({
        "role": "user",
        "content": user
    })

    # AIに送信
    response = client.responses.create(
        model="gpt-4.1-mini",
        input=messages
    )

    ai_reply = response.output_text

    # 表示
    print("\nAI:", ai_reply, "\n")

    # ログ保存
    chat_log.append(f"[{now}] AI: {ai_reply}")

    # 履歴に追加（記憶用）
    messages.append({
        "role": "assistant",
        "content": ai_reply
    })

    # 履歴が長くなりすぎたら整理（軽量化）
    if len(messages) > 20:
        messages = [messages[0]] + messages[-15:]
