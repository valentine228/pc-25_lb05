# pc-25_lb05
### Обновление системы:
<img width="716" height="511" alt="image" src="https://github.com/user-attachments/assets/88baf195-3f54-4e68-91aa-1d3d6726f916" />

### Установка Python и OpenSSL:
<img width="736" height="560" alt="image" src="https://github.com/user-attachments/assets/12638480-fc3a-482c-a865-1663a1b9cb86" />

### Создание виртуального окружения:
<img width="683" height="156" alt="image" src="https://github.com/user-attachments/assets/27366a7d-d615-4333-bbfb-48c65a7952a0" />

### Установка библиотек
<img width="747" height="522" alt="image" src="https://github.com/user-attachments/assets/ff57b8a6-b788-40d5-b178-68168d51f72a" />

### Генерация сертификатов и ключей и генерация ключа шифрования. Создание инфраструктуры PKI для mTLS аутентификации. Сертификаты позволяют серверу и клиенту идентифицировать друг друга. Создаем симметричный ключ для шифрования данных алгоритмом Fernet. Один ключ используется для шифрования (клиент) и расшифровки (сервер).
<img width="737" height="555" alt="image" src="https://github.com/user-attachments/assets/776a2dd5-c333-49a9-86b6-c997b235f66c" />

### Запуск серверов 1,2; запуск координатора; запуск клиентов 1,2 (порядок слева направо).
<img width="1614" height="551" alt="image" src="https://github.com/user-attachments/assets/516c0b1f-ca20-478e-b85f-c1857eb6b1c6" />

## Вариант 6
def get_data():
    try:
        data = request.get_json().get('data')
        if not data:
            return {'error': 'Data not provided'}, 400
        # Decrypt data
        decrypted_data = decrypt_data(data)
        # Process decrypted data
        print(f"Decrypted data: {decrypted_data.decode()}")
        return {'result': 'ok'}
    except Exception as e:
        return {'error': str(e)}, 400

 --- Новый эндпоинт для получения кэшированных данных (НЕ требует аутентификацию)---
@app.route('/api/get_cached_data', methods=['GET']) # Используем GET для получения данных
def get_cached_data_endpoint():
    data = get_cached_data_logic()
    # Возвращаем JSON с результатом
    return jsonify({'status': 'success', 'data': data})

 --- Опциональный эндпоинт для инвалидации кэша (может требовать аутентификацию или быть внутренним)---
 Для простоты сделаем его без аутентификации, но на практике это может быть защищено
@app.route('/api/invalidate_cache', methods=['POST'])
def post_invalidate_cache_endpoint():
    invalidate_cache_logic()
    return jsonify({'status': 'success', 'message': 'Cache invalidated on this server instance.'})
