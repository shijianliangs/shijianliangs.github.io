---
title: "golang_http_client_demo"
date: 2019-10-24
categories: ["go"]
tags: ["go"]
draft: false 
---
# golang http client demo

```go
package main

import (
	"crypto/tls"
	"encoding/json"
	"fmt"
	"io/ioutil"
	"net/http"
	"net/url"
	"strings"
	"time"
)

func main() {
	// simple Get
	response, err := http.Get("https://www.baidu.com")
	if err != nil {
		fmt.Println(err)
	}
	defer response.Body.Close()
	bytes, err := ioutil.ReadAll(response.Body)
	if err != nil {
		fmt.Println(err)
	}
	contents := string(bytes)
	fmt.Println(contents)

	// simple Post Form
	params := url.Values{
		"P1": {"p1"},
		"P2": {"p2"},
	}
	response, err = http.Post("https://www.baidu.com", "application/x-www-form-urlencoded", strings.NewReader(params.Encode()))
	if err != nil {
		fmt.Println(err)
	}
	defer response.Body.Close()
	bytes, err = ioutil.ReadAll(response.Body)
	if err != nil {
		fmt.Println(err)
	}
	contents = string(bytes)
	fmt.Println(contents)

	// simple Post Json
	marshal, err := json.Marshal(map[string]interface{}{
		"P1": "p1",
		"P2": "p2",
	})
	if err != nil {
		fmt.Println(err)
	}
	response, err = http.Post("https://www.baidu.com", "application/json", strings.NewReader(string(marshal)))
	if err != nil {
		fmt.Println(err)
	}
	defer response.Body.Close()
	bytes, err = ioutil.ReadAll(response.Body)
	if err != nil {
		fmt.Println(err)
	}
	contents = string(bytes)
	fmt.Println(contents)

	// request with header cookie and ignore ssl
	marshal, err = json.Marshal(map[string]interface{}{
		"P1": "p1",
		"P2": "p2",
	})
	if err != nil {
		fmt.Println(err)
	}
	request, err := http.NewRequest(http.MethodPost, "https://www.baidu.com", strings.NewReader(string(marshal)))
	if err != nil {
		fmt.Println(err)
	}
	request.AddCookie(&http.Cookie{
		Name:       "C1",
		Value:      "c1",
		Path:       "/",
		Domain:     "www.baidu.com",
		Expires:    time.Time{},
		RawExpires: "",
		MaxAge:     0,
		Secure:     false,
		HttpOnly:   false,
		SameSite:   0,
		Raw:        "",
		Unparsed:   nil,
	})
	request.Header.Add("Content-Type", "application/json")
	client := http.Client{Transport: &http.Transport{TLSClientConfig: &tls.Config{InsecureSkipVerify: true}}} // ignore ssl
	defer client.CloseIdleConnections()
	response, err = client.Do(request)
	if err != nil {
		fmt.Println(err)
	}
	defer response.Body.Close()
	bytes, err = ioutil.ReadAll(response.Body)
	if err != nil {
		fmt.Println(err)
	}
	contents = string(bytes)
	fmt.Println(contents)
}

```