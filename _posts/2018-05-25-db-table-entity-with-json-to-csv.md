---
layout: post
title: DB table entity with json to csv
date: 2018-05-25 13:37 +0000
---


```php
$entities = DB::table('temp')->get()->toArray();

        $writer = Writer::createFromFileObject(new \SplTempFileObject());

        $writer->setDelimiter('|');
        $writer->setEncodingFrom('utf-8');


        $writer->insertOne([
            'email',
            'first_name',
            'last_name',
            'user_textarea',
            'gender',
            'age',
            'children',
            'hobbies',
            'terms',
            'created_at',
        ]);

        $dataSet = [];
        foreach ($entities as $entity) {
            $data = [];
            $data[] = $entity->email;
            $data[] = $entity->first_name;
            $data[] = $entity->last_name;

            $json = \GuzzleHttp\json_decode($entity->value, true);

            if (isset($json['user_textarea'])) {
                $data[] = $json['user_textarea'];
            } else {
                $data[] = 'N/A';
            }

            if (isset($json['gender'])) {
                $data[] = $json['gender'];
            } else {
                $data[] = 'N/A';
            }

            if (isset($json['age'])) {
                $data[] = $json['age'];
            } else {
                $data[] = 'N/A';
            }

            if (isset($json['children'])) {
                $data[] = $json['children'];
            } else {
                $data[] = 'N/A';
            }

            if (isset($json['hobbies'])) {
                $data[] = implode(',', $json['hobbies']);
            } else {
                $data[] = 'N/A';
            }

            if (isset($json['terms'])) {
                $data[] = implode(',', $json['terms']);
            } else {
                $data[] = 'N/A';
            }

            $data[] = $entity->created_at;

            $dataSet[] = $data;
        }
        Storage::disk('local')->put('-txt2.csv', $writer->insertAll($dataSet));


        echo $writer->__toString();
        static::assertTrue(true);
```
