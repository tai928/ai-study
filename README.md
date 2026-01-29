from openai import OpenAI

client = OpenAI(api_key="YOUR_KEY")

response = client.chat.completions.create(
    model="gpt-4o-mini",
    messages=[
        {"role":"system","content":"You are a helpful assistant"},
        {"role":"user","content":"こんにちは"}
    ]
)

print(response.choices[0].message.content)
